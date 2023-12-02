from pyModis import MODIS_data
import numpy as np
import matplotlib.pyplot as plt

# Specify the spatial and temporal extents of your study
spatial_extent = dict(lonmin=-120, lonmax=-70, latmin=30, latmax=60)
temporal_extent = dict(start_date='2020-01-01', end_date='2020-12-31')

# Create an instance of the MODIS_data class
modis_data = MODIS_data(spatial_extent, temporal_extent)

# Download the MODIS data
modis_data.download_MODIS_data(data_source='MCD12Q1', var_list=['pftBiomass', 'pftLAI', 'pftHeight'])

# Extract the variables of interest from the downloaded data
biomass_data = modis_data.get_MODIS_variable(var_name='pftBiomass')
lai_data = modis_data.get_MODIS_variable(var_name='pftLAI')
height_data = modis_data.get_MODIS_variable(var_name='pftHeight')

# Analyze the data as needed, e.g., calculate the average vegetation height across the study area
average_vegetation_height = np.nanmean(height_data)

# Plot the data, e.g., display the average vegetation height over time
time_array = modis_data.get_MODIS_time_array()
plt.plot(time_array, average_vegetation_height)
plt.xlabel('Time')
plt.ylabel('Average Vegetation Height')
plt.title('Average Vegetation Height Over Time')
plt.show()
