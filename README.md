# Community Cadastre Mapping Revolution

## Table of Contents
1. [Download Software](#one-download-software)
2. [Mapping with QGIS](#two-using-qgis-to-map-the-geospatial-data)
3. [Machine Learning with Jupyter Notebooks](#three-using-jupyter-notebooks-to-do-the-machine-learning-building-age-predictions)
4. [Uploading Data to Felt](#four-using-felt-to-upload-the-data)

---

## ONE: Download Software
- **Download QGIS**: Get the latest version from [QGIS.org](https://www.qgis.org/en/site/forusers/download.html)
- **Download QGIS plugins**
  - MMQGIS

---

## TWO: Using QGIS to Map the Geospatial Data

### Getting Started
- **Download files**: Rename the downloaded files as `a_boundary`, `b_land`, etc.

### Projection
- **Ensure Correct Projection**: Use British National Grid (BNG - 27700)

### Data Cleaning

#### Wards
- Select only the relevant ward (i.e., Meadows)
- Remove unnecessary columns from the attribute table

#### Land Polygons

##### Location
- Select land polygons only in the relevant ward
- Use 'Select by Location' to choose polygons that intersect with `a_boundary`

##### Size
- Find out the area of the largest single dwelling piece of land
- Filter polygons with `Area > 1283` and remove them
- Remove unnecessary columns from the attribute table

#### Building Polygons
- Use the field expression calculator to filter house-related buildings  
  `"building" = 'detached' OR "building" = 'house' OR "building" = 'residential' OR "building" = 'semidetached_house' OR "building" = 'terrace' OR 'building' = 'yes'`

#### Additional Steps
- Invert feature selection and delete non-residential features
- Make layer editable and delete extra large houses (`Area > 244`)
- Select garages by feature type and remove them

#### Attribute Editing
- Add an attribute named `Private`
  1. Open attribute table
  2. Make layer editable
  3. Open attribute field calculator
  4. Create a boolean field with the expression `overlay_intersects (ncc_owned_layer)`

#### Spatial Join
- Use MMQGIS -> Combine -> Spatial Join
- Output as a new layer called `cadastre`

#### Final Steps
- Calculate building-to-land ratio using attribute table
- Save changes to the layer
- Export layer as `.csv` (save as `cadastre_output`)
- Manually label some data based on available archetype maps or visual survey

---

## THREE: Using Jupyter Notebooks to Do the Machine Learning Building Age Predictions
- Follow the instructions in the provided Jupyter Notebook.

---

## FOUR: Using Felt to Upload the Data
- Register for a free account at [Felt.com](https://www.felt.com)
- Use their drag-and-drop system to upload your data.

See your community cadastre take shape!

