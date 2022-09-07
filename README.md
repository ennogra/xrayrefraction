# REFRAC: a toolbox to calculate X-ray refraction of matter
This Matlab toolbox calculates the refraction properties of a matter under X-ray radiation (energy range 0.03~30 KeV), such as dispersion, absorption parts of the index of refraction, the critical angle of total external reflection, attenuation length etc. It basically does the same thing as CXRO X-Ray Interactions With Matter. However, the advantage is that the toolbox does not require internet access, and you can directly use it in your Matlab script.

Caution: CXRO includes Compton scattering when calculating the absorption length, while Refrac does not. The difference becomes obvious for materials of light elements when energy is >10 Kev.

For example, the following script plots dispersion and absorption of SiO2 for X-ray energies between 0.1-10 KeV:

```Matlab
x = 10.^linspace(log10(0.1), log10(10), 1000);           % list of X-ray energies (KeV)
y = refrac('SiO2', x, 2.648);                                         % give chemical formula and mass density to calculate properties of SiO2
loglog(x*1000, y.dispersion, x*1000, y.absorption);    % plot in eV
```

![refrac](http://1.bp.blogspot.com/-7CEbjcKl2gE/VYRCPw2djiI/AAAAAAAAAmQ/KlW_eVTulLo/s1600/sio2.jpg)

This standalone toolbox is included in GIXSGUI toolbox. However, you can download and run it separately. After downloading, remember to choose "Add with Subfolders" in Matlab "Set Path" to include the main and all subfolders to Matlab search path; otherwise, the toolbox will not work.

For more information about X-ray interactions with matter, go to [NIST](http://www.nist.gov/pml/data/ffast/index.cfm) and [LBL](http://www.cxro.lbl.gov/). 

For usage, in Matlab command window, type ">>help refrac".

refrac  Material property when interacting with x-rays.

     Usage: result = refrac(Chemical Formula,Energy,MassDensity)

     Input:
        1) Chemical formula. Can be either cell array (for multiple
           formulas) or single string. Formula is case sensitive (e.g. CO
           for Carbon Monoxide vs Co for Cobalt);
        2) Energy (0.03KeV~30KeV). Can be single or list.
        3) List of mass densities (g/cm^3);
    
     Output: Can be either cell of structures (if input formular is cell
        array) or single structure (if input is single string) with the
        following elements:
        1) Chemical formula;
        2) Molecular weight;
        3) Number of electrons per molecule;
        4) Mass density (g/cm^3);
        5) Electron density (1/A^3);
        6) X-ray energy (KeV);
        7) Corresponding X-ray wavelength (A);
        8) Dispersion;
        9) Absorption;
        10) Critical angle (degree);
        11) Attenuation length (cm);
        12) Real part of scattering length density (SLD) (A^-2);
        13) Imaginary part of SLD (A^-2).

     Example 1: >> result=refrac({'H2O','Si3N4'},8.04778,[1,3.44])
                Output: cell of structures
                result{2} =
                  chemFormula: 'Si3N4'
              molecularWeight: 140.28
            numberOfElectrons: 70
                  massDensity: 3.44
              electronDensity: 1.0337
                       energy: 8.0478
                   wavelength: 1.5406
                   dispersion: 1.1164e-005
                   absorption: 1.6477e-007
                criticalAngle: 0.27074
                    attLength: 0.0074403
                        reSLD: 2.9554e-005
                        imSLD: 4.362e-007
    
     Example 2: >>result=refrac('SiO2',8:0.5:10,2.33)
                Output: structure
                result =
                  chemFormula: 'SiO2'
              molecularWeight: 60.0843
            numberOfElectrons: 30
                  massDensity: 2.33
              electronDensity: 0.7006
                       energy: [5x1 double]
                   wavelength: [5x1 double]
                   dispersion: [5x1 double]
                   absorption: [5x1 double]
                criticalAngle: [5x1 double]
                    attLength: [5x1 double]
                        reSLD: [5x1 double]
                        imSLD: [5x1 double]    
