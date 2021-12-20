# areal_interpolation_tutorial
Performing and assessing areal interpolation methods using Tobler


* **Ottawa census tracts (`data/ottawa_ct_pop_2016.gpkg`)**
  * Geometry source: 
    * [StatCan 2016 Census: Census Tracts Cartographic Boundary File](https://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/bound-limit-2016-eng.cfm)
  * Geometry transformations:
    * Extracted the census tracts falling within the City of Ottawa boundary
    * Reprojected to WGS 84 UTM 18N
  * Attributes source:
    * [StatCan 2016 Census: Census metropolitan areas (CMAs), tracted census agglomerations (CAs) and census tracts (CTs)](https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/details/download-telecharger/comp/page_dl-tc.cfm?Lang=E&)
  * Attributes transformations:
    * Extracted the 'Population, 2016' data ('member ID 1) for the City of Ottawa census tracts
    * Joined to the census tracts geometry


* **Ottawa dissemination areas (`data/ottawa_da_pop_2016.gpkg`)**
  * Geometry source: 
    * [StatCan 2016 Census: Dissemination Areas Cartographic Boundary File](https://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/bound-limit-2016-eng.cfm)
  * Geometry transformations:
    * Extracted the dissemination areas falling within the City of Ottawa boundary
    * Reprojected to WGS 84 UTM 18N
  * Attributes source:
    * [Canada, provinces, territories, census divisions (CDs), census subdivisions (CSDs) and dissemination areas (DAs) - Ontario only](https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/details/download-telecharger/comp/page_dl-tc.cfm?Lang=E&)
  * Attributes transformations:
    * Extracted the 'Population, 2016' data ('member ID 1) for the City of Ottawa dissemination areas
    * Joined to the dissemination areas geometry

* **Ottawa neighborhoods**
  * Source:
    * [Ottawa Neighbourhood Study (ONS) - Neighbourhood Boundaries Gen 2](https://open.ottawa.ca/datasets/ottawa::ottawa-neighbourhood-study-ons-neighbourhood-boundaries-gen-2/about)
  * Geometry transformations:
    * Reprojected to WGS 84 UTM 18N
  * Attributes transformations:
    * Extracted the neighborhood names and estimated population fields
