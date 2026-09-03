# Body Fat Prediction Dataset

## Overview

This dataset contains estimates of the percentage of body fat determined by underwater weighing and various body circumference measurements for **252 men**. The dataset is designed to illustrate multiple regression techniques for predicting body fat percentage using simple, non-invasive measurements.

## Context

Accurate measurement of body fat is inconvenient and costly (requiring underwater weighing), making it desirable to have easy methods of estimating body fat that are not inconvenient or costly. This dataset allows researchers to develop predictive equations using simple body circumference measurements that can be easily obtained.

## Source

**Data Provider**: Dr. A. Garth Fisher  
**Permission**: Data freely distributed for non-commercial purposes

**Contact**:  
Roger W. Johnson  
Department of Mathematics & Computer Science  
South Dakota School of Mines & Technology  
501 East St. Joseph Street  
Rapid City, SD 57701  

**Email**: rwjohnso@silver.sdsmt.edu  
**Web**: http://silver.sdsmt.edu/~rwjohnso

## Variable Descriptions

### Target Variables

1. **Density** (numeric)
   - Body density determined from underwater weighing
   - Measured in grams per cubic centimeter (gm/cm³)
   - Range: approximately 0.995 to 1.109 gm/cm³
   - **Note**: This is the primary measurement from underwater weighing

2. **BodyFat** (numeric)
   - Percent body fat from Siri's (1956) equation
   - Calculated using: **Percentage of Body Fat = 495/Density - 450**
   - Measured as percentage
   - Range: approximately 0% to 47.5%

### Demographic Variables

3. **Age** (numeric)
   - Age in years
   - Range: 22 to 81 years

### Anthropometric Variables

4. **Weight** (numeric)
   - Body weight
   - Measured in pounds (lbs)
   - Range: approximately 118.5 to 363.1 lbs

5. **Height** (numeric)
   - Body height
   - Measured in inches
   - Range: approximately 29.5 to 77.75 inches

### Body Circumference Measurements

All circumference measurements are in centimeters (cm) and follow the measurement standards listed in Behnke and Wilmore (1974), pp. 45-48.

6. **Neck** (numeric)
   - Neck circumference (cm)

7. **Chest** (numeric)
   - Chest circumference (cm)

8. **Abdomen** (numeric)
   - Abdomen 2 circumference (cm)
   - **Measurement**: Laterally, at the level of the iliac crests, and anteriorly, at the umbilicus
   - This is often one of the most predictive measurements for body fat

9. **Hip** (numeric)
   - Hip circumference (cm)

10. **Thigh** (numeric)
    - Thigh circumference (cm)

11. **Knee** (numeric)
    - Knee circumference (cm)

12. **Ankle** (numeric)
    - Ankle circumference (cm)

13. **Biceps** (numeric)
    - Biceps (extended) circumference (cm)

14. **Forearm** (numeric)
    - Forearm circumference (cm)

15. **Wrist** (numeric)
    - Wrist circumference (cm)

## Body Fat Calculation: Siri's Equation

The percentage of body fat is calculated from body density using Siri's equation, which is based on the two-component model of body composition:

### Two-Component Model

The body is assumed to consist of two components:
- **Lean body tissue** (density = 1.10 gm/cm³)
- **Fat tissue** (density = 0.90 gm/cm³)

### Mathematical Derivation

Let:
- **D** = Body Density (gm/cm³)
- **A** = proportion of lean body tissue
- **B** = proportion of fat tissue (A + B = 1)
- **a** = density of lean body tissue (1.10 gm/cm³)
- **b** = density of fat tissue (0.90 gm/cm³)

Then:
```
D = 1/[(A/a) + (B/b)]
```

Solving for B (proportion of fat):
```
B = (1/D) × [ab/(a-b)] - [b/(a-b)]
```

### Siri's Equation

Using the estimates a = 1.10 gm/cm³ and b = 0.90 gm/cm³:

**Percentage of Body Fat = 495/D - 450**

This equation converts body density to percentage body fat.

## Underwater Weighing Method

Body density is accurately measured using underwater weighing:

### Principle

Body volume is computed as the difference between body weight measured in air and weight measured during water submersion. Body volume equals the loss of weight in water with appropriate temperature correction for the water's density.

### Formula

```
Body Density = WA/[(WA-WW)/c.f. - LV]
```

Where:
- **WA** = Weight in air (kg)
- **WW** = Weight in water (kg)
- **c.f.** = Water correction factor
  - = 1 at 39.2°F (one gram of water occupies exactly one cm³ at this temperature)
  - = 0.997 at 76-78°F
- **LV** = Residual Lung Volume (liters)

## Research Application

### Original Research

These data were used to produce predictive equations for lean body weight in the abstract:

**"Generalized body composition prediction equation for men using simple measurement techniques"**  
K.W. Penrose, A.G. Nelson, A.G. Fisher, FACSM  
Human Performance Research Center, Brigham Young University, Provo, Utah 84602  

Published in: **Medicine and Science in Sports and Exercise**, vol. 17, no. 2, April 1985, p. 189
