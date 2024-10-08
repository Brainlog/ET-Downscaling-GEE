# Overview of the code available

## Downscaling(Using Landsat-7) and calibration of ET

The downscaling ET code provided within this folder ``Calibration\`` are different in the sense that they use Landsat-7 variables instead of Landsat-8.

We thought of leveraging exisiting ET datasets to come up with an ET product at a much finer resolution. In our research, we use
the MODIS product. We aimed at generating ET rasters at a temporal resolution of 1-8
days and a spatial resolution of 30 metres and were successful in doing so.

Once ET at a finer resolution was predicted using machine learning based approaches
we found a need to calibrate it against the Indian Meteorological Department’s or IMD’s
data(ground truth). We also used climatic variables like, temperature, humidity, soil moisture, precipitation as input features when we generated models for calibration.

The model for ET downscaling(provided in this repository) using Landsat-7 values was generated as follows:
  1. In the ``Calibration\Downscaling ET\Colab Scripts\ExportTrainData.ipynb`` file update the train_areas_aez_1to5 variable so that it contains the Earth Engine FeatureCollection ``Calibration\Data\aez_train_areas.csv`` provided with this repository(You will need to first load the CSV onto Google Earth Engine to be able to import it for using it in the script).
2. Run the script and it will upload a CSV for each year. These CSVs will have the data for all the training patches for different time periods.
3. Once the training data is exported, the ``Calibration\Downscaling ET\Colab Scripts\modelTrain&Upload_ET.ipynb`` file will use the training data and train a model and upload the same on earth engine.
4. The same model can then be loaded on Earth Engine and the code in the ``Calibration\Downscaling ET\GEE Scripts\Downscale_ET_Inference.js`` file can be used to make predictions for the downscaled data.
5. Sample models for the same have already been provided in the ``Calibration\Data`` folder. ``Calibration\Data\landsat_8_rf_model.csv`` is the earlier Random Forest model that was trained on Landsat 8 features. Similarly ``Calibration\Data\updated_landsat_7_rf_model.csv`` is the Random Forest model trained using the Landsat 7 Features

Once the Downscaled ET is generated, we can move ahead and try calibrating it to the different regions of India as follows:
1. Load the ``Calibration\Calibrating ET\Colab Scripts\K_Fold_Regression_Github.ipynb`` file on google colab.
2. Upload the ``Calibration\Calibrating ET\Colab Scripts\ET_Version_2.xlsx`` file on colab and run different cells for different types of regression models to get different graphs and visualizations of how different models fare against each other.
