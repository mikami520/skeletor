# News

## 1.3.0 (2023-03-31)

New post-processing methods:
- `skeletor.post.smooth` to smooth the skeleton
- `skeletor.post.despike` remove spikes from skeleton
- `skeletor.post.remove_bristles` to remove single-node bristles from the skeleton

## 1.2.0 (2022-04-03)

This release mainly improves `skeletor.skeletonize.by_wavefront` but it also
adds a new method to get a graph representation of skeletons:
`Skeleton.get_graph`.

## 1.1.0 (2021-07-26)

This is a small release that adds a single method to the `Skeleton` class to
quickly save results as
[SWC](http://www.neuronland.org/NLMorphologyConverter/MorphologyFormats/SWC/Spec.html)
file:

```Python
>>> skel.to_swc('skeleton.swc')
```

## 1.0.0 (2021-04-09)

This release represents a major rework of `skeletor`. Notably, functions that
were previously exposed at top level (e.g. `skeletor.contract`) have been
moved to submodules sorting them by their purpose:

| < 1.0.0                     | >= 1.0.0                  |
| --------------------------- | ------------------------- |
| `skeletor.fix_mesh`         | `skeletor.pre.fix_mesh`   |
| `skeletor.simplify`         | `skeletor.pre.simplify`   |
| `skeletor.remesh`           | `skeletor.pre.remesh`     |
| `skeletor.contract`         | `skeletor.pre.contract`   |
| `skeletor.cleanup`          | `skeletor.post.clean_up`  |
| `skeletor.radii`            | `skeletor.post.radii`     |

Similarly `skeletor.skeletonize(method='some method')` has been broken out into
separate functions:

| < 1.0.0                                                | >= 1.0.0                                             |
| ------------------------------------------------------ | ---------------------------------------------------- |
| `skeletor.skeletonize(mesh, method='vertex_clusters')` | `skeletor.skeletonize.by_vertex_clusters(mesh)`      |
| `skeletor.skeletonize(mesh, method='edge_collapse')`   | `skeletor.skeletonize.by_edge_collapse(mesh)`        |


### New Features
- new skeletonization methods `skeletor.skeletonize.by_tangent_ball`,
  `skeletor.skeletonize.by_wavefront` and `skeletor.skeletonize.by_teasar`
- all skeletonization functions return a `Skeleton` object that bundles the
  results (SWC, nodes/vertices, edges, etc.) and allows for quick visualization
- SWC tables are now strictly conforming to the format (continuous node IDs,
  parents always listed before their childs, etc)
- `Skeleton` results contain a mesh to skeleton mapping as `.mesh_map` property
- added an example mesh: to load it use `skeletor.example_mesh()`
- `skeletor` now has proper tests and a simple [documentation](https://navis-org.github.io/skeletor/)

### Removals
- removed `drop_disconnected` parameter from all skeletonization functions -
  pleases either use `fix_mesh` to remove small disconnected pieces from the
  mesh or drop those in postprocessing
- `output` parameter has been removed from all skeletonization functions as the
  output is now always a `Skeleton`


### Bugfixes
- plenty
