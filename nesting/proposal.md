# WIP Model Nesting: Proposal

At present, SDFormat adds an `<include/>` tag. However, it has the following
design issues:

1.   Encapsulation, Lifetime: There is no specification on how encapsulated an included file should be, and at what stage of construction inclusion is permitted.
    * Can the included file refer to joints that it does not define?
        * Example: Adding a gripper to an IIWA. There may be a weld pose based on the pneumatic or electric flange.
    * It is useful to encode frame offsets.
2.   There is no explicit specification about namespacing, relative references or absolute references, etc.
    * This is being addressed in the [Pose Frame Semantics Proposal PR](https://bitbucket.org/osrf/sdf_tutorials/pull-requests/7/pose-frame-semantics-proposal-for-new/diff)
3.   SDFormat requires that included models be converted to SDFormat (e.g. including an URDF). This may prevent software packages from doing more complex composition where there may not be an exact mapping to SDFormat, or where this conversion is excessive overhead.

## Lifetime

```xml
<!-- Toy Robot -->
<model name="robot">
    ...
    <link name="final_link">...</link>
    <frame name="end_effector">
        <pose frame="final_link">...</pose>
    </frame>
</model>

<!-- Electric Flange -->
<!-- NOTE: PURELY kinematic. Only defines frames. -->
<model name="electric_flange">
    <frame name="
</model>

<!-- Toy Gripper -->
<model name="gripper">
    ...
</model>
```

Proposed welding semantics:
```xml
<!-- Electric Gripper Frame -->
<model name="robot_with_gripper">
    <include></include>
</model>
```



## Encapsulation


