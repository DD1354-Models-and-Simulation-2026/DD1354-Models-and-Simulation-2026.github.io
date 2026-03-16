# DD1354-Models-and-Simulation-2026.github.io
DD1354 project blog.

# Week 8 and before

We considered multiple ways to set up the project. At first, we looked at physically based algorithms that simulate a crack going through an object, we set up simple simulations of these to get an idea of the feasibility of implementing such algorithms. We concluded after some testing that a physically based simulation would be too complicated considering the limited scope of the class.  

<img width="945" height="489" alt="image" src="https://github.com/user-attachments/assets/e2e0eb9e-ee41-4029-82cc-6d4c6b3f0d53" />

Simple VIP python code using LEFM (linear elastic fracture mechanics).


We also tried to gauge what evaluation methods exist in this field, and it seems to be a limited number of ways to measure success of any implementation. The main ways are visual feasibility, performance (time to fracture an amount of shards) and more complicated algorithms that measure the distribution of shards in a fractured objects regarding size and location of the shards. 


# Week 9

We set up a comparison scene in Unity containing two glass panels:

Glass_OpenFracture: using the default OpenFracture implementation.                                                             
Glass_Voronoi: our experimental version where we generate Voronoi cells.

We successfully integrated a Voronoi diagram generator using the GK library together with Oskar Sigvardsson’s Delaunay implementation. The Voronoi cells are currently generated dynamically and rendered on top of the glass surface using a LineRenderer.

At this stage, the Voronoi version does not yet physically fracture the mesh. Instead, it visualizes the Voronoi cell structure that will later be used to drive the fracturing process.

This establishes the foundation for replacing the default OpenFracture slicing logic with a Voronoi-based fragmentation approach.

 <img width="600" height="348" alt="image" src="https://github.com/user-attachments/assets/2f17ba2a-5333-43d7-b187-90a9f98aee19" />



Next, we implemented an impact-based Voronoi visualization for the glass in our comparison scene.

Previously, Voronoi cells were generated randomly across the entire glass surface. Now the Voronoi diagram is calculated dynamically based on the collision point when a ball hits the glass. We retrieve the impact point from “OnCollisionEnter” and generate more seeds near the impact point to simulate a more realistic crack formation.

The result is that the Voronoi cells are concentrated around the collision area, which visually resembles how cracks in glass spread from a point of impact. This step is an very important part of our extended implementation because it creates a more physically plausible crack structure compared to a completely random fragmentation. Currently, only the Voronoi structure is visualized with LineRenderer. The actual mesh fracturing based on these cells will be implemented in the next steps.
<img width="610" height="403" alt="image" src="https://github.com/user-attachments/assets/c5d1deec-25f1-44ea-a694-3d6de62ee881" />



We further experimented with integrating the Voronoi cells with the slicing system used in OpenFracture. The goal was to use the generated Voronoi cells to directly drive the mesh fracturing. However, we encountered some issues. Some Voronoi cells disappeared during the slicing process, and the number of generated cells did not always match the number of seeds specified in the Inspector. Resolving these issues would require significant refactoring of the code.

Because of these difficulties, we temporarily decided to focus on visualizing the Voronoi structure first before continuing with the full mesh fracturing implementation.



At the end of week 9, we decided to restructure the project to more clearly understand what needed to be done and how we should proceed.

After our experiments with integrating Voronoi with the OpenFractures slicing system, several uncertainties arose regarding the implementation. Therefore, we created a new priority list to structure the work and focus on the most critical parts of the project.

The images below show some early tests of fragmentation during this phase.
<img width="611" height="787" alt="image" src="https://github.com/user-attachments/assets/41806f97-693b-4d58-a793-16c556aa9b17" />


# Week 10


Our priority was to implement local fracturing and handle cracks in the glass that are not part of detached shards. The process of implementing local fracturing initially behaved incorrectly.
<img width="646" height="418" alt="image" src="https://github.com/user-attachments/assets/82026463-0ee3-42d4-bd12-6bafb5e0097b" />


Not only were new “glass slices” created, but the original ones did not break either, which resulted in a stack of overlapping glass slices.


## Project Proposal

<iframe src="ProjectProposal.pdf" width="100%" height="800px" style="border: 1px solid #ccc;"></iframe>
