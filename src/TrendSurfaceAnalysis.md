# **Enhanced Trend Surface Analysis Plugin Documentation**

## **Overview**

The **Enhanced Trend Surface Analysis Plugin** is a powerful QGIS tool for spatial trend analysis using polynomial regression. It allows users to model spatial patterns in point data and generate trend surfaces with comprehensive statistical diagnostics.

## **Table of Contents**

1. [Features](#features)
2. [Installation](#installation)
3. [Quick Start](#quick-start)
4. [User Interface](#user-interface)
5. [Parameters Explained](#parameters-explained)
6. [Outputs](#outputs)
7. [Use Cases](#use-cases)
8. [Troubleshooting](#troubleshooting)
9. [Mathematical Background](#mathematical-background)
10. [FAQ](#faq)

## **Features**

### **Core Analysis**
- **Polynomial Trend Surfaces**: Degrees 1-8 for flexible modeling
- **Least Squares Regression**: Robust mathematical foundation
- **Multiple Output Formats**: Raster surfaces and point residuals
- **Automatic CRS Handling**: Maintains coordinate reference systems

### **Advanced Capabilities**
- **Robust Regression**: Outlier-resistant analysis
- **Cross-Validation**: Model performance validation
- **Confidence Intervals**: Uncertainty quantification
- **Comprehensive Statistics**: R², RMSE, AIC, BIC, and more

### **User Experience**
- **Intuitive Interface**: Easy-to-use dialog-based workflow
- **Automatic Field Detection**: Smart field name recognition
- **Real-time Feedback**: Progress monitoring and logging
- **Automatic Styling**: Pre-configured layer symbology

## **Installation**

### **System Requirements**
- QGIS 3.16 or later
- Python 3.7+
- NumPy, SciPy libraries (included with QGIS)

### **Installation Steps**

1. **Download the Plugin**
   ```bash
   # Clone from repository or download ZIP
   git clone https://github.com/your-repo/enhanced-trend-surface.git
   ```

2. **Install in QGIS**
   - Open QGIS
   - Go to `Plugins → Manage and Install Plugins`
   - Click `Install from ZIP`
   - Select the plugin directory or ZIP file
   - Click `Install Plugin`

3. **Verify Installation**
   - Check for "Enhanced Trend Surface" in the Plugins menu
   - Look for the plugin icon in the toolbar

### **Manual Installation**
```bash
# Copy to QGIS plugins directory
cp -r EnhancedTrendSurface ~/.local/share/QGIS/QGIS3/profiles/default/python/plugins/
```

## **Quick Start**

### **Basic Workflow**
1. **Load your point data** with elevation/Z values
2. **Click the plugin icon** or go to `Plugins → Enhanced Trend Surface → Enhanced Trend Surface Analysis`
3. **Select input layer** and Z value field
4. **Choose analysis parameters** (polynomial degree, cell size)
5. **Set output locations** for results
6. **Click "Run Analysis"** and view results

### **Example: Topographic Analysis**
1. Load a point layer with elevation data
2. Set polynomial degree to 2 (quadratic surface)
3. Use 100m cell size for output raster
4. Run analysis to visualize regional topography

## **User Interface**

### **Main Dialog Components**

#### **Input Parameters Section**
- **Input Point Layer**: Dropdown of all point layers in project
- **Z Value Field**: Numeric field containing values to analyze
- **Weight Field** (optional): Field for weighted regression
- **Polynomial Degree**: Complexity of trend surface (1-8)
- **Cell Size**: Resolution of output raster in map units
- **Confidence Level**: Statistical confidence for intervals (80-99.9%)

#### **Analysis Options**
- **Cross-Validation**: Enable k-fold validation for model assessment
- **Robust Regression**: Use outlier-resistant fitting method

#### **Output Settings**
- **Trend Surface**: Main output raster (required)
- **Residuals Surface**: Difference between observed and predicted (optional)
- **Confidence Intervals**: Uncertainty surface (optional)
- **Statistics Folder**: Location for detailed reports (optional)

## **Parameters Explained**

### **Polynomial Degree**
| Degree | Equation Terms | Use Case |
|--------|---------------|----------|
| 1 | 3 (planar) | Simple linear trends |
| 2 | 6 (quadratic) | Gentle curvature, basic topography |
| 3 | 10 (cubic) | Complex surfaces, geological features |
| 4+ | 15+ | Highly complex patterns (use with caution) |

**Recommendation**: Start with degree 2-3 for most applications.

### **Cell Size**
- **Small values** (1-10m): High detail, larger files
- **Medium values** (10-100m): Balanced detail and performance
- **Large values** (100-1000m): Regional trends, faster processing

### **Confidence Level**
- **90%**: Standard scientific use
- **95%**: Common statistical threshold
- **99%**: High certainty requirements

## **Outputs**

### **Generated Layers**

#### **1. Trend Surface Raster**
- **Description**: Continuous surface showing spatial trend
- **Symbology**: Blue-to-red color ramp (low to high values)
- **Use**: Primary visualization of spatial pattern

#### **2. Residual Points Layer**
- **Description**: Original points with residual values
- **Fields**: 
  - Original attributes
  - `residual`: Observed - Predicted
  - `predicted`: Model-predicted value
- **Use**: Identify local anomalies and model fit

#### **3. Residuals Surface Raster** (Optional)
- **Description**: Interpolated residual values
- **Symbology**: Diverging blue-white-red (negative-zero-positive)
- **Use**: Spatial pattern of model errors

#### **4. Confidence Intervals Raster** (Optional)
- **Description**: Standard error of predictions
- **Symbology**: Grayscale (light to dark = low to high uncertainty)
- **Use**: Assess prediction reliability

### **Statistical Reports**

#### **Comprehensive Statistics**
```text
ENHANCED POLYNOMIAL TREND SURFACE ANALYSIS REPORT
==================================================

Analysis Date: 2024-01-15 14:30:25
Polynomial Degree: 2
Number of Observations: 250
Number of Parameters: 6

GOODNESS OF FIT STATISTICS:
R²: 0.8743
Adjusted R²: 0.8712
RMSE: 12.45
MAE: 8.67

MODEL SELECTION CRITERIA:
AIC: 1456.23
BIC: 1478.45

RESIDUAL ANALYSIS:
Residual Mean: 0.0234
Residual Std: 12.38
Normality Test p-value: 0.2345

CROSS-VALIDATION RESULTS:
CV R²: 0.8621
CV MSE: 156.34
Folds Completed: 5
```

## **Use Cases**

### **1. Topographic Analysis**
- **Data**: Elevation points, LiDAR data
- **Degree**: 2-3
- **Output**: Regional slope and aspect patterns
- **Application**: Watershed delineation, terrain analysis

### **2. Environmental Monitoring**
- **Data**: Pollution measurements, temperature readings
- **Degree**: 1-2
- **Output**: Pollution gradients, thermal patterns
- **Application**: Environmental impact assessment

### **3. Geological Applications**
- **Data**: Mineral concentrations, rock properties
- **Degree**: 2-4
- **Output**: Geological trend surfaces
- **Application**: Resource exploration, geological mapping

### **4. Climate Studies**
- **Data**: Precipitation, temperature stations
- **Degree**: 1-3
- **Output**: Climate surfaces
- **Application**: Climate modeling, agricultural planning

## **Troubleshooting**

### **Common Issues**

#### **"Insufficient points" Error**
- **Cause**: Too few points for selected polynomial degree
- **Solution**: 
  - Collect more data points
  - Reduce polynomial degree
  - Minimum points = (degree + 1) × (degree + 2) ÷ 2

#### **"Matrix solving failed" Error**
- **Cause**: Numerically unstable design matrix
- **Solution**:
  - Reduce polynomial degree
  - Check for duplicate points
  - Ensure adequate spatial distribution

#### **Poor Model Fit (Low R²)**
- **Causes**:
  - Insufficient polynomial complexity
  - High local variability
  - Outliers influencing model
- **Solutions**:
  - Increase polynomial degree
  - Enable robust regression
  - Remove spatial outliers

### **Performance Tips**

#### **For Large Datasets**
- Use larger cell sizes initially
- Start with lower polynomial degrees
- Enable robust regression for noisy data

#### **For Complex Patterns**
- Gradually increase polynomial degree
- Use cross-validation to prevent overfitting
- Compare multiple degree results

## **Mathematical Background**

### **Polynomial Trend Surface**

A polynomial trend surface of degree *d* is defined as:

```
z(x,y) = β₀ + β₁x + β₂y + β₃x² + β₄xy + β₅y² + ... + βₙyᵈ
```

Where:
- `z(x,y)` is the predicted value at coordinates (x,y)
- `βᵢ` are the coefficients determined by regression
- The number of terms = `(d + 1) × (d + 2) ÷ 2`

### **Least Squares Regression**

The coefficients are determined by minimizing the sum of squared residuals:

```
min Σ(z_observed - z_predicted)²
```

Solved using the normal equations:
```
β = (AᵀA)⁻¹Aᵀz
```

Where `A` is the design matrix of polynomial terms.

### **Robust Regression**

Uses iteratively reweighted least squares with Huber weighting:
```
w_i = min(1, k / |r_i|)
```
Where `r_i` are residuals and `k` is a tuning constant.

## **FAQ**

### **Q: What's the difference between degree 1, 2, and 3?**
- **Degree 1**: Planar surface (flat plane)
- **Degree 2**: Curved surface with one inflection
- **Degree 3**: Complex surface with multiple inflection points

### **Q: When should I use robust regression?**
Use robust regression when your data contains outliers or when you want to reduce their influence on the trend surface.

### **Q: How many points do I need?**
Minimum points = number of polynomial terms + 10. For degree 2 (6 terms), aim for at least 16 points.

### **Q: Can I use this for categorical data?**
No, the plugin is designed for continuous numeric data. For categorical data, consider classification methods.

### **Q: Why are my residuals clustered spatially?**
Spatial clustering of residuals suggests local effects not captured by the global trend. Consider local interpolation methods for these areas.

### **Q: How do I interpret R² values?**
- 0.0-0.3: Weak fit
- 0.3-0.7: Moderate fit  
- 0.7-0.9: Strong fit
- 0.9-1.0: Excellent fit

## **Advanced Usage**

### **Batch Processing**
For multiple datasets, consider using the Python API:

```python
from EnhancedTrendSurface.core_analysis import TrendSurfaceAnalyzer

analyzer = TrendSurfaceAnalyzer()
results = analyzer.analyze(layer, 'elevation', degree=3, cell_size=50)
```

### **Custom Styling**
Modify the automatic styling by editing the style functions in the plugin code.

## **Support and Development**

### **Getting Help**
- **Documentation**: This guide
- **Issues**: GitHub issue tracker
- **Community**: QGIS user forums

### **Contributing**
We welcome contributions! Areas for improvement:
- Additional regression methods
- 3D visualization support
- Time-series trend analysis
- Enhanced export options

### **Citation**
If you use this plugin in research, please cite:
```
S. S. Goveia. Enhanced Trend Surface Analysis Plugin for QGIS. Version 1.0. 
Spatial Analysis Tools. 2025.
```

---

**Note**: This documentation is for version 1.0 of the Enhanced Trend Surface Analysis Plugin. Check for updates and new features in subsequent releases.
