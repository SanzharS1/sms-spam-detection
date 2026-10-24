# Use Case diagram artifacts

[use_case.dot](use_case.dot) is the editable Graphviz source; [use_case.svg](use_case.svg) is its readable vector export. The actor/use-case definitions and scenarios are documented in [UX Scenarios](../docs/ux_scenarios.md). The diagram describes proposed behavior, including restricted offline operations; it is not an implementation result.

Open the SVG in a browser and zoom for inspection, or insert it as a vector image into the report. Actor rectangles use UML classifier notation with the `«actor»` keyword. Solid associations, hollow-triangle actor generalization, dashed `«include»` and dashed `«extend»` relationships have different meanings; see the scenario document for conditions and extension points.

With Graphviz installed, regenerate the export from the repository root:

```powershell
neato -Tsvg diagrams/use_case.dot -o diagrams/use_case.svg
```

An optional raster export for report tools that cannot import SVG can be generated with:

```powershell
neato -Tpng -Gdpi=180 diagrams/use_case.dot -o diagrams/use_case.png
```

The SVG was rendered from the DOT source using the `neato` engine of the Graphviz WebAssembly implementation in `@viz-js/viz`. Positions are pinned in the source to keep related goals together. Native Graphviz versions may produce different text metrics; compare labels and relationships after regeneration. The temporary rendering dependency is not an application dependency.

Before accepting an updated export, check that all 13 `UC-` labels and five actors are readable, every oval stays within the system boundary, associations do not imply data flow, the generalization triangle points toward SMS user, include arrows point toward UC-02, and the optional contribution arrow points from UC-08 toward UC-07. Model/evaluation maintenance and system operation are separate roles, matching the System Context. Check the SVG at useful report size and keep source/export in the same change. A teammate must separately review requirement and architecture alignment.
