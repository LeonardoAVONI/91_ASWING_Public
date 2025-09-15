## ASWING Official Documentation
### Quick Introduction
[ASWING](https://web.mit.edu/drela/Public/web/aswing/) is a computational tool developed at MIT by **Mark Drela** for the **aerodynamic, structural, and control analysis of aircraft**.  
It is designed for **time-domain** or **frequency-domain** simulation of **flexible aircraft dynamics**; and it allows users to investigate both **steady and unsteady flight mechanics**.  

Comprehensive documentation and theoretical background (steady and unsteady formulations) are available on the [official ASWING page](https://web.mit.edu/drela/Public/web/aswing/), along with sample input files and example calculations.


### License Information

ASWING is proprietary software owned by **MIT** and distributed by the **MIT Technology Licensing Office (TLO)**.  

- **Academic / Student use**: A license must be requested (free for non-commercial academic use).  
- **Commercial use**: Requires a commercial license through MIT TLO.  

📄 License request form and conditions: [ASWING EULA (MIT TLO)](https://tlo.mit.edu/sites/default/files/2023-11/ASWING_EULA_noncommercial_2021_05%20%281%29.pdf)  
🔗 MIT TLO ASWING page: [ASWING Technology Overview](https://tlo.mit.edu/industry-entrepreneurs/available-technologies/aswing-software-aerodynamic-structural-and-control)  

For licensing inquiries, contact:  
- Email: [software-licenses@mit.edu](mailto:software-licenses@mit.edu)  
- Phone: +1 (617) 253-6966  


**Note**: It is your responsibility to obtain and comply with the appropriate license from MIT and Prof. Mark Drela before using ASWING.

---



## Romain Jan Validation Work
ASWING has been extensively validated in the PhD work of **Romain Jan**,  
titled *"Récupération d'énergie sur drone à voilure souple"* (*Energy Recovery for Flexible Wing UAV*)  
([thesis link](https://theses.fr/2023ESAE0046), [PDF](https://depozit.isae.fr/theses/2023/2023_Jan_Romain.pdf)).

Throughout his thesis, Jan systematically compared **ASWING predictions** with **experimental measurements** and **high-order CFD simulations**, providing a detailed assessment of the software’s reliability for aeroelastic and flight mechanics applications.  
The validation effort is documented both in his thesis and in a dedicated series of four reports:

- **Part I: Aerodynamics**  
  [Experimental validation of an aeroelasticity framework – ASWING, Part I](https://www.researchgate.net/publication/377724794_Experimental_validation_of_an_aeroelasticity_framework_ASWING_Part_I_Aerodynamics)

- **Part II: Propellers**  
  [Experimental validation of an aeroelasticity framework – ASWING, Part II](https://www.researchgate.net/publication/377725378_Experimental_validation_of_an_aeroelasticity_framework_ASWING_Part_II_Propellers)

- **Part III: Structure**  
  [Experimental validation of an aeroelasticity framework – ASWING, Part III](https://www.researchgate.net/publication/377725277_Experimental_validation_of_an_aeroelasticity_framework_ASWING_Part_III_Structure)

- **Part IV: Aeroelasticity**  
  [Experimental validation of an aeroelasticity framework – ASWING, Part IV](https://www.researchgate.net/publication/377725388_Experimental_validation_of_an_aeroelasticity_framework_ASWING_Part_IV_Aeroelasticity)

---

Together, these works provide a **comprehensive benchmark** of ASWING against trusted experimental and computational references, strengthening confidence in its predictive capabilities for flexible aircraft dynamics.
## ASWING ISAE-Supaero/ENAC Documentation

[Project Report](./documents/05_ASWING_Leonardo_s_Report.pdf)

## WingLoop Extension
Through the PhD of Leonardo AVONI, a code allowing 

![My Project Logo](./documents/WingLoop.png)

## Other Notes
Michael Kapteyn developed Aswing.py
A Python wrapper for ASWING, accessible here
https://github.com/michaelkapteyn/Aswing.py

Although existing, this code was not used 