<h1 style="text-align: center;">Initial Steps Towards an Open Cadastre in the UK: A Case Study</h1>

# 1. The Meadows Community Cadastre

[Take a closer look](https://felt.com/map/The-Meadows-Community-Cadastre-zSR9C9CHsOSSy9BIRiv9Ayx4OD?loc=52.939297,-1.145295,17.9z&share=1)
<p align="center">
<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExOGYwdXRnMzlvdDEwdmFnaWtyMXZ3d3duZ3cwdHRzcWhvNmc0ZnUwNCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/YHoKsbmM2UfMdqc3xu/giphy.gif" width="50%" />
</p>

<p align="center">
<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExNjlya2xxb2hpMnUzOTlhMHI1ejI2NGZpY29mZXlkanhtdGx3azE1MSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/dbZOkmNgi1HgpsNtBs/giphy.gif" width="50%" />
</p>

<p align="center">
<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExcGFuMTEwcGNkMjVtd3FzdDV4bjRkY290dnBoYjliaDhydmFtMHJpdCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ojUq32cEHHYj39DwBW/giphy.gif" width="50%" />
</p>

</div>


## 2. Create your own Community Cadastre


## Table of Contents
STEP 1. [Download the Open Source Software](#one-download-software)
STEP 2. [Mapping with QGIS](#two-using-qgis-to-map-the-geospatial-data)
STEP 3. [Machine Learning in Jupyter Notebooks to Predict Building Age](#three-using-jupyter-notebooks-to-do-the-machine-learning-building-age-predictions)
STEP 4. [Uploading Data to Felt](#four-using-felt-to-upload-the-data)

---

## STEP 1: Download the Open Source Software
- **Download QGIS**: Get the latest version from [QGIS.org](https://www.qgis.org/en/site/forusers/download.html)
- **Download QGIS plugins**: Get the latest version from [MichaelMinn.com](https://michaelminn.com/linux/mmqgis/)

---

## STP 2: Using QGIS to Map the Geospatial Data

### Getting Started
- **Download files**: Rename the downloaded files as `a_boundary`, `b_land`, etc. to be your new layers, and rearrange them as required.

### Projection
- **Ensure Correct Projection**: Transform your local British data layers to British National Grid (BNG - 27700).

### Data Cleaning

#### Wards
- From the Local Authority Ward Boundaries, select only the relevant ward(s) (i.e., Meadows)
- Remove any unnecessary columns from the attribute table, as this will slow down the processing and be unuseful to users viewing the map.

#### Land Polygons

##### Location
- Select land polygons that are in the area of interest.
- Use 'Select by Location' to choose polygons that intersect with `a_boundary`.

##### Size
- Find out the area of the largest single-dwelling piece of land.
- Filter polygons with `Area > 1283` and remove them.
- Remove unnecessary columns from the attribute table.

#### Building Polygons
- Use the field expression calculator to filter house-related buildings
  `"building" = 'detached' OR "building" = 'house' OR "building" = 'residential' OR "building" = 'semidetached_house' OR "building" = 'terrace' OR 'building' = 'yes'`

#### Additional Steps
- Invert feature selection and delete non-residential features.
- Make the layer editable and delete extra large houses (`Area > 244`).
- Select garages by feature type and remove them.

#### Attribute Editing
- Add an attribute named `Private`.
  1. Open the attribute table
  2. Make the layer editable
  3. Open the attribute field calculator
  4. Create a boolean field with the expression `overlay_intersects (ncc_owned_layer)`

#### Spatial Join
- Use MMQGIS -> Combine -> Spatial Join
- Output as a new layer called `cadastre`

#### Final Steps
- Calculate the building-to-land ratio using the attribute table
- Save changes to the layer
- Export layer as `.csv` (save as `cadastre_output`)
- Manually label some data based on available archetype maps or visual survey

---

## STEP 3: Machine Learning in Jupyter Notebooks to Predict Building Age
- For full details run the code, and read the comments in the notebooks.
- But start off here by downloading the code and running locally:
<br>
Clone the directory

```
$ git clone [https://github.com/InfobyAdrienne/Test-React-Express.git](https://github.com/99ltaylor/community_cadastre.git)
```

---

## STEP 4: Using Felt to Upload the Data
- Register for a free account at [Felt.com](https://www.felt.com)
- Use their drag-and-drop file system to upload your data.

See your community cadastre take shape!

