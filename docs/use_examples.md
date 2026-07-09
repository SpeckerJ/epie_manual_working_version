## The PEPPER model

ePiE stands out for its high degree of customizability. Most parameters can be overwritten, allowing users to use experimental data or other models such as PEPPER (Predict Environmental Pollutant PERsistence).

The PEPPER model was developed using large-scale monitoring data from WWTP applying secondary treatment with activated sludge and covers over 1000 chemicals applying a random-forest model to predict the WWTP breakthrough of anthropogenic chemicals. These predictions are based on the chemical structure alone and also allow to asses their half-life in soil. PEPPER is freely accessible as a web application via the following [link](https://pepper-app.streamlit.app/). More information on the PEPPER model can be found under the web application or in its respective publication by [Cordero Solano et al. (2025)](https://pubs.acs.org/doi/full/10.1021/acs.est.5c09314).

To use PEPPER, please follow the points outlined below:

1. Go to the PEPPER website
2. Click on "Single Molecule" (Figure 1)



    <img src="../img/screenshots/PEPPER/pepper_screen1.png" alt="img1" style="width: 100%; max-width: 600px; height: 50%;" />
    <figcaption>Figure 1</figcaption>


3. Choose "WWTP breakthrough" as endpoint to predict (Figure 2)


    <img src="../img/screenshots/PEPPER/pepper_screen2.png" alt="img1" style="width: 100%; max-width: 600px; height: 50%;" />
    <figcaption>Figure 2</figcaption>


4. Choose one of the example chemicals, such as Sulfamethoxazole (Option 1), or provide the SMILES (Option 2) (Figure 3) 
5. Click "OK" (Figure 3)


    <img src="../img/screenshots/PEPPER/pepper_screen3.png" alt="img1" style="width: 100%; max-width: 600px; height: 50%;" />
    <figcaption>Figure 3</figcaption>


PEPPER calculates the breakthrough (%) of a compound, which is the fraction of a compound that is *not* removed (Figure 4). ePiE, however, requires the removed fraction. Accordingly, the breakthrough needs to be converted to the removed fraction. For example, PEPPER calculates a breakthrough of 50.2 % for sulfamethoxazole, which translates to 49.8 % removal. This value can be used under the "WWTP removal" tab as input value for either the primary or secondary removal fraction. For example, by setting the primary removal fraction to 0, and the secondary removal fraction to 0.498. PEPPER also provides a confidence metric and results close to 0 should be used with care!

