---
layout: single
title: "OCCT : 4. 모델 그리기(Custom)"
description: OCCT 모델 그리기
categories:
 - opencascade
---

Bulit-in된 Interactive Object를 지원하지 않는 경우, `AIS_InteractiveObject`를 상속 받아, 해당 지오메트리의 렌더링 표현 방식을 정의할 수 있다.

### AIS_Curve 구현

```cpp
// AIS_Curve.h
/// <summary>
/// ais object for curve <para/>
/// https://dev.opencascade.org/doc/overview/html/tutorials__ais_object.html#intro
/// </summary>
class AIS_Curve : public AIS_InteractiveObject    
{
    /// <summary>
    /// DEFINE_STANDARD_RTTI_INLINE() macro will register the new class within the OCCT Run-Time Type Information (RTTI) system.
    /// This step is optional (you may skip it if you are not going to use methods like Standard_Transient::DynamicType() in application code), 
    /// but it is a common practice while subclassing OCCT classes.
    /// </summary>
    DEFINE_STANDARD_RTTI_INLINE(AIS_Curve, AIS_InteractiveObject)

public:
    AIS_Curve(const Handle(Geom_Curve)& curve);

    /// <summary>
    /// defining an object presentation
    /// </summary>
    virtual void Compute(const Handle(PrsMgr_PresentationManager)& thePrsMgr,
        const Handle(Prs3d_Presentation)& thePrs,
        const Standard_Integer theMode) override;

    /// <summary>
    /// defining a selectable (pickable) volume
    /// </summary>
    /// <param name="theSelection"></param>
    /// <param name="theMode"></param>
    virtual void ComputeSelection(const Handle(SelectMgr_Selection)& theSelection,
        const Standard_Integer theMode) override {}

private:
    Handle(Geom_Curve) _curve;
};
```

```cpp
// AIS_Curve.cpp
AIS_Curve::AIS_Curve(const Handle(Geom_Curve)& curve)
    : _curve(curve)
{

}

void AIS_Curve::Compute(const Handle(PrsMgr_PresentationManager)& thePrsMgr,
    const Handle(Prs3d_Presentation)& thePrs,
    const Standard_Integer theMode) {

    GeomAdaptor_Curve adaptorCurve = GeomAdaptor_Curve(_curve);
    myDrawer->SetLineAspect(new Prs3d_LineAspect(Quantity_NOC_RED, Aspect_TOL_SOLID, 1.0));
    StdPrs_Curve::Add(thePrs, adaptorCurve, myDrawer);
}
```

![image](https://github.com/Jay1127/OCCT_Samples/assets/38006679/a7124419-fca8-4115-9772-1e3c9eb01d34){: .align-center}

### AIS_Solid 구현

```cpp
// AIS_Solid.h
class AIS_Solid : public AIS_InteractiveObject
{
    /// <summary>
    /// DEFINE_STANDARD_RTTI_INLINE() macro will register the new class within the OCCT Run-Time Type Information (RTTI) system.
    /// This step is optional (you may skip it if you are not going to use methods like Standard_Transient::DynamicType() in application code), 
    /// but it is a common practice while subclassing OCCT classes.
    /// </summary>
    DEFINE_STANDARD_RTTI_INLINE(AIS_Solid, AIS_InteractiveObject)

public:
    AIS_Solid(const TopoDS_Shape& shape);

    /// <summary>
    /// defining an object presentation
    /// </summary>
    virtual void Compute(const Handle(PrsMgr_PresentationManager)& thePrsMgr,
        const Handle(Prs3d_Presentation)& thePrs,
        const Standard_Integer theMode) override;

    /// <summary>
    /// defining a selectable (pickable) volume
    /// </summary>
    /// <param name="theSelection"></param>
    /// <param name="theMode"></param>
    virtual void ComputeSelection(const Handle(SelectMgr_Selection)& theSelection,
        const Standard_Integer theMode) override {}

private:
    TopoDS_Shape _shape;
};
```

```cpp
// AIS_Solid.cpp
AIS_Solid::AIS_Solid(const TopoDS_Shape& shape) 
    : _shape(shape)
{
    
}

void AIS_Solid::Compute(const Handle(PrsMgr_PresentationManager)& thePrsMgr,
    const Handle(Prs3d_Presentation)& thePrs,
    const Standard_Integer theMode)
{
    if (theMode == 0) {
        StdPrs_ShadedShape::Add(thePrs, _shape, myDrawer);
    }
    else if (theMode == 1) {
        StdPrs_WFShape::Add(thePrs, _shape, myDrawer);
    }
    else if (theMode == 2) {
        StdPrs_ShadedShape::Add(thePrs, _shape, myDrawer);
        StdPrs_WFShape::Add(thePrs, _shape, myDrawer);
    }
}
```

![image](https://github.com/Jay1127/OCCT_Samples/assets/38006679/1cc30b79-3741-4f94-aefc-89a5c4ad9fdb){: .align-center}