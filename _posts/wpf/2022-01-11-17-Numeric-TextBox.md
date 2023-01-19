---
layout: single
title: "WPF : 17. TextBox에 숫자만 입력하는 법"
description: TextBox에 숫자만 입력하는 법
categories:
 - WPF
---

## 방법 1. 입력되는 문자가 숫자인지 판단

- 정규표현식을 이용해서 입력된 문자가 `0 ~ 9, . , -`인 경우에만 `TextBox`에 반영한다.
- 하지만, 이 방법은 `TextBox`에 `12-.2`와 같은 문자가 입력될 수도 있다.

```csharp
public class NumericInputTextBox
{
    public static readonly DependencyProperty IsNumericInputProperty =
        DependencyProperty.RegisterAttached("IsNumericInput", typeof(bool), typeof(NumericInputTextBox),
        new PropertyMetadata(false, new PropertyChangedCallback(OnIsNumericInputChanged)));

    public static bool GetIsNumericInput(DependencyObject obj)
    {
        return (bool)obj.GetValue(IsNumericInputProperty);
    }

    public static void SetIsNumericInput(DependencyObject obj, bool value)
    {
        obj.SetValue(IsNumericInputProperty, value);
    }

    private static void OnIsNumericInputChanged(DependencyObject d, DependencyPropertyChangedEventArgs e)
    {
        if (d is TextBox textBox)
        {
            if ((bool)e.NewValue)
            {
                textBox.Unloaded += TextBox_Unloaded;
                textBox.PreviewTextInput += OnPreviewTextInput;
            }
            else
            {
                textBox.Unloaded -= TextBox_Unloaded;
                textBox.PreviewTextInput -= OnPreviewTextInput;
            }
        }
    }

    private static void TextBox_Unloaded(object sender, RoutedEventArgs e)
    {
        var textBox = sender as TextBox;
        textBox.PreviewTextInput -= OnPreviewTextInput;
    }

    private static void OnPreviewTextInput(object sender, TextCompositionEventArgs e)
    {
        e.Handled = !IsNumeric(e.Text);
    }

    public static bool IsNumeric(string source)
    {
        // 입력문자가 0 ~ 9, . , - 가 아닌게 하나라도 있는 경우 숫자 아니라고 판단
        var regex = new Regex("[^0-9.-]+");

        return !regex.IsMatch(source);
    }
}
```

## 방법 2. 입력된 후의 문자열이 숫자인지 판단

- 입력 후 문자열이 숫자인지 판단하여, 숫자인 경우 `TextBox`에 반영한다.

```csharp
public class NumericInputTextBox
{
    public static readonly DependencyProperty IsNumericInputProperty =
        DependencyProperty.RegisterAttached("IsNumericInput", typeof(bool), typeof(NumericInputTextBox),
        new PropertyMetadata(false, new PropertyChangedCallback(OnIsNumericInputChanged)));

    public static bool GetIsNumericInput(DependencyObject obj)
    {
        return (bool)obj.GetValue(IsNumericInputProperty);
    }

    public static void SetIsNumericInput(DependencyObject obj, bool value)
    {
        obj.SetValue(IsNumericInputProperty, value);
    }

    private static void OnIsNumericInputChanged(DependencyObject d, DependencyPropertyChangedEventArgs e)
    {
        if (d is TextBox textBox)
        {
            if ((bool)e.NewValue)
            {
                textBox.Unloaded += TextBox_Unloaded;
                textBox.PreviewTextInput += OnPreviewTextInput;
            }
            else
            {
                textBox.Unloaded -= TextBox_Unloaded;
                textBox.PreviewTextInput -= OnPreviewTextInput;
            }
        }
    }

    private static void TextBox_Unloaded(object sender, RoutedEventArgs e)
    {
        var textBox = sender as TextBox;
        textBox.PreviewTextInput -= OnPreviewTextInput;
    }

    private static void OnPreviewTextInput(object sender, TextCompositionEventArgs e)
    {
        var textBox = sender as TextBox;

        // 입력 완료된 문자열 찾기
        var text = textBox.Text;
        for (int i = textBox.SelectionStart + textBox.SelectedText.Length - 1; i >= textBox.SelectionStart; i--)
        {
            text = text.Remove(i, 1);
        }

        text = text.Insert(textBox.SelectionStart, e.Text);

        // 입력 완료된 문자열이 숫자인 경우만 TextBox에 반영
        e.Handled = !double.TryParse(text, out double _);
    }
}
```