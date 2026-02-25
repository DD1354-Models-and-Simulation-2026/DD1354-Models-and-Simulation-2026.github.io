# DD1354-Models-and-Simulation-2026.github.io
DD1354 project blog.

We set up a comparison scene in Unity containing two glass panels:

Glass_OpenFracture: using the default OpenFracture implementation.                                                             
Glass_Voronoi: our experimental version where we generate Voronoi cells.

We successfully integrated a Voronoi diagram generator using the GK library together with Oskar Sigvardsson’s Delaunay implementation. The Voronoi cells are currently generated dynamically and rendered on top of the glass surface using a LineRenderer.

At this stage, the Voronoi version does not yet physically fracture the mesh. Instead, it visualizes the Voronoi cell structure that will later be used to drive the fracturing process.

This establishes the foundation for replacing the default OpenFracture slicing logic with a Voronoi-based fragmentation approach.

 <img width="600" height="348" alt="image" src="https://github.com/user-attachments/assets/2f17ba2a-5333-43d7-b187-90a9f98aee19" />

## Project Proposal

<iframe src="ProjectProposal.pdf" width="100%" height="800px" style="border: 1px solid #ccc;"></iframe>
