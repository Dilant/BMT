---
outline:
  level: 2
---

# Road Generator

- The editor provides 7 road generator algorithms: `Road`, `Corner`, `Wood Board`, `Rail`, `Tube`, `Custom Vertices`, `Custom Script`.
- In [`Start → Road Generator`](../../start/roadGenerator), the basic usage of the road generator has been introduced, and some examples were provided.
- The various properties of the road generator are quite intuitive. It is recommended to experiment hands-on, adjusting each property yourself to understand its function and effect.
- For road generator algorithms already introduced in the Start section, only their properties, types, and default values are listed here, without extensive explanation.
- Click to jump to the usage of the [`Custom Vertices`](#Custom-Vertices) road generator.
- The [`Custom Script`](../../script/roadGenerator) road generator will be introduced in the `Script` section.
- A more advanced road generator: [`Way Point Road Generator`](#Way-Point-Road-Generator).

::: details Bending Algorithm

```py
def skeletonGenerator(
    length: float,
    height: float,
    bend: EulerAngle,
    segment: int
) -> tuple[list[Vector3], list[EulerAngle]]:

    segment_length: float = length / segment
    segment_height: float = height / segment
    point_posture_delta: EulerAngle = bend / segment
    segment_direction_delta: EulerAngle = bend / segment / 2
    point_positions: list[Vector3] = [Vector3(0, 0, 0)]
    point_postures: list[EulerAngle] = [EulerAngle(0, 0, 0)]

    for i in range(1, segment + 1):
        segment_direction: EulerAngle = (2 * i - 1) * segment_direction_delta
        point_position: Vector3 = (
            point_positions[-1]
            + segment_direction * Vector3(0, 0, segment_length)
            + Vector3(0, segment_height, 0)
        )
        point_posture: EulerAngle = i * point_posture_delta
        point_positions.append(point_position)
        point_postures.append(point_posture)

    return point_positions, point_postures

```

:::

## Quick Functions

The `Road Generator` component provides 3 quick functions:

- `Clone`: Creates an identical road at the end of the current road and automatically sets its rotation and other properties.
- `Generate`: Forcibly refreshes the current road generator. For a [`Custom Script`](../../script/roadGenerator) road generator, you can click this button to refresh the generated result after modifying the script.
- `Create Way Point`: Creates [`Way Point`](wayPoint) at the corresponding positions based on the current road generator's segments.

## Road

::: details Road

### `Length`

- Type: `float`
- Default: `4.0`

### `Width`

- Type: `float`
- Default: `1.0`

### `End Width`

- Type: `float`
- Default: `1.0`

### `End Height`

- Type: `float`
- Default: `0.0`

### `End Offset`

- Type: `float`
- Default: `0.0`

### `Thickness`

- Type: `float`
- Default: `1.0`

### `Segments`

- Type: `int`
- Default: `1`
- Range: `1` ~ `256`

### `Bend`

- Type: `Float3`
- Default: `(0, 0, 0)`

### `Create Cap`

- Type: `bool`
- Default: `true`

### `Precise UV Length`

- Type: `bool`
- Default: `false`

### `Rotate Main UV`

- Type: `bool`
- Default: `false`

### `Main UV Offset`

- Type: `Float2`
- Default: `(0, 0)`

### `Sides UV Offset`

- Type: `float`
- Default: `0.0`

### `Concave`

- Type: `float`
- Default: `0.0`

### `End Concave`

- Type: `float`
- Default: `0.0`

:::

## Corner

::: details Corner

### `Size`

- Type: `float`
- Default: `1.0`

### `Thickness`

- Type: `float`
- Default: `1.0`

### `Create Cap`

- Type: `bool`
- Default: `true`

### `Rotate Main UV`

- Type: `bool`
- Default: `false`

### `Main UV Offset`

- Type: `Float2`
- Default: `(0, 0)`

### `Concave`

- Type: `float`
- Default: `0.0`

:::

## Wood Board

::: details Wood Board

### `Length`

- Type: `float`
- Default: `4.0`

### `Width`

- Type: `float`
- Default: `1.0`

### `End Height`

- Type: `float`
- Default: `0.0`

### `End Offset`

- Type: `float`
- Default: `0.0`

### `Thickness`

- Type: `float`
- Default: `1.0`

### `Segments`

- Type: `int`
- Default: `1`
- Range: `1` ~ `256`

### `Bend`

- Type: `Float3`
- Default: `(0, 0, 0)`

### `Create Cap`

- Type: `bool`
- Default: `true`

### `Precise UV Length`

- Type: `bool`
- Default: `false`

### `Rotate Main UV`

- Type: `bool`
- Default: `false`

### `Main UV Offset`

- Type: `Float2`
- Default: `(0, 0)`

### `Sides UV Offset`

- Type: `float`
- Default: `0.0`

:::

## Rail

::: details Rail

### `Length`

- Type: `float`
- Default: `4.0`

### `Offsets`

- Type: `Float2[]`
- Default: `[(-0.38, 0), (0.38, 0)]`

### `End Height`

- Type: `float`
- Default: `0.0`

### `End Offset`

- Type: `float`
- Default: `0.0`

### `Segments`

- Type: `int`
- Default: `1`
- Range: `1` ~ `256`

### `Rotation Segments`

- Type: `int`
- Default: `8`
- Range: `1` ~ `128`

Number of segments in the rail's cross-section.

### `Rotation Offset`

- Type: `float`
- Default: `0.0`
- Range: `-180` ~ `180`

Rotation angle of the rail's cross-section.

### `Bend`

- Type: `Float3`
- Default: `(0, 0, 0)`

### `Create Cap`

- Type: `bool`
- Default: `true`

### `Precise UV Length`

- Type: `bool`
- Default: `false`

### `Main UV Offset`

- Type: `Float2`
- Default: `(0, 0)`

### `Radius`

- Type: `float`
- Default: `0.06`

The cross-sectional radius (thickness) of the rail.

:::

## Tube

::: details Tube

### `Length`

- Type: `float`
- Default: `4.0`

### `End Height`

- Type: `float`
- Default: `0.0`

### `End Offset`

- Type: `float`
- Default: `0.0`

### `Radius`

- Type: `float`
- Default: `0.5`

### `End Radius`

- Type: `float`
- Default: `0.5`

### `Slice`

- Type: `Float2`
- Default: `(0, 360)`

The `Start Angle` and `End Angle` of the tube's cross-section.

### `Thickness`

- Type: `float`
- Default: `0.05`

### `Segments`

- Type: `int`
- Default: `1`
- Range: `1` ~ `256`

### `Rotation Segments`

- Type: `int`
- Default: `16`
- Range: `1` ~ `128`

Number of segments in the tube's cross-section.

### `Bend`

- Type: `Float3`
- Default: `(0, 0, 0)`

### `Create Cap`

- Type: `bool`
- Default: `true`

### `Precise UV Length`

- Type: `bool`
- Default: `false`

### `Main UV Offset`

- Type: `Float2`
- Default: `(0, 0)`

:::

## Custom Vertices

- `Vertices Group`: Each vertices group corresponds to a section of the road.
- `Vertices`: Each vertex corresponds to a point coordinate in the **XY plane**.
  - `Position`: The position coordinate of the vertex, with the **item's position** as the origin.
  - `UV`: The UV coordinate of the vertex.

::: tip

- Different sections of the road can have different materials.
- Custom vertices roads **cannot** have caps created.
- Please ensure that the first and last vertices in each vertices group are connected.
- The UV coordinates of two adjacent vertices should not be the same.

:::

::: details Custom Vertices

### `Length`

- Type: `float`
- Default: `4.0`

### `End Height`

- Type: `float`
- Default: `0.0`

### `End Offset`

- Type: `float`
- Default: `0.0`

### `Segments`

- Type: `int`
- Default: `1`
- Range: `1` ~ `256`

### `Bend`

- Type: `Float3`
- Default: `(0, 0, 0)`

### `Precise UV Length`

- Type: `bool`
- Default: `false`

### `Rotate Main UV`

- Type: `bool`
- Default: `false`

### `Main UV Offset`

- Type: `Float2`
- Default: `(0, 0)`

:::

## Custom Script

The [`Custom Script`](../../script/roadGenerator) road generator will be introduced in the `Script` section.

## Way Point Road Generator

Currently, the waypoint road generator is only effective for `Road` and `Wood Board`.

It is recommended to first read the content related to the [`Way Point`](wayPoint) and [`Way Path`](wayPath) components.

Usage:

1. Create some `Way Points` and, in the `Hierarchy`, drag these `Way Points` into the `Road Generator` item to make them its children.
2. On the `Road Generator` item, enable the `Way Path` component and check `Auto Collect`. The path will now automatically collect all `Way Points` from its children.
3. Depending on your needs, choose whether to check `Use Curve` and `Closed Path`.
4. In the `Road Generator` component, adjust the `Segments` property.
5. At this point, only the `Thickness`, `Concave`, and `End Concave` properties in the `Road Generator` component will have an effect; the rest are controlled by the `Way Points`.
6. Adjust the `Position`, `Rotation`, and `Scale` properties of each `Way Point` to shape the road.
