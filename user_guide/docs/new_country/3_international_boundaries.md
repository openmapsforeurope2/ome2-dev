# Define international boundaries for OME2

For the OME2 project, in order to harmonise data across countries, it is necessary to use common international boundaries. However, neighbouring countries often provide different geometries for their international boundaries, even when these are officially agreed.

An FME workbench was therefore put into place to calculate common “technical” boundaries, which are considered as a reference for the project: boundary_unification_process

> TO-DO: move to boundary_unification doc
> - When an isolated country is integrated, only the first step of the workbench needs to be used. This creates the boundary lines (including coastlines) all around the country.
> - Then the lines need to be split manually where there is a change in country code or boundary type (international boundary vs coastline).
> - Create point in ib.international_boundary_node when there is a change in the boundary line (type or country code).
> - Use EBM as reference.
