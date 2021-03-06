# SFI-MVLEM-3D
three-dimensional, four-node, macroscopic element for RC walls with shear-flexural interaction

[K. Kolozvari](mailto:kkolozvari@fullerton.edu), CSU Fullerton<br/>
K. Kalbasi, CSU Fullerton<br/>
K. Orakcal, Bogazici University<br/>
L. M. Massone, University of Chile, Santiago<br/>
J. W. Wallace, UCLA<br/>

## Description

The SFI-MVLEM-3D model (Figure 1a) is a three-dimensional four-node element with 24 DOFs that incorporates axial-flexural-shear interaction and can be used for nonlinear analysis of non-rectangular reinforced concrete walls subjected to multidirectional loading. The SFI-MVLEM_3D model is an extension of the two-dimensional, two-node Shear-Flexure-Interaction Multiple-Vertical-Line-Element-Model ([SFI-MVLEM](https://opensees.berkeley.edu/wiki/index.php/SFI_MVLEM_-_Cyclic_Shear-Flexure_Interaction_Model_for_RC_Walls)). The baseline SFI-MVLEM, which is essentially a line element for rectangular walls subjected to in-plane loading, is extended in this study to a three-dimensional model formulation by applying geometric transformation of the element degrees of freedom that converted it into a four-node element formulation (Figure 1b), as well as by incorporating linear elastic out-of-plane behavior based on the Kirchhoff plate theory (Figure 1c). The in-plane and the out-of-plane element behaviors are uncoupled in the present model.


![Model_Formulation](https://user-images.githubusercontent.com/53920372/94061362-21147080-fd9a-11ea-8a73-f325dc96206a.JPG)
**Figure 1: SFI-MVLEM-3D Element Formulation**

### SFI-MVLEM-3D Input
```markdown
element SFI_MVLEM_3D eleTag iNode jNode kNode lNode m  -thick {Thicknesses} -width {Widths} -mat {Material_tags} 
<-CoR c> <-ThickMod tMod> <-Poisson Nu>  <-Density Dens>
```

| parameter | description |
|----------|------------|
| eleTag | unique element tag|
| iNode jNode kNode lNode | tags of element nodes defined in counterclockwise direction|
| m | number of element macro-fibers|
| {Thicknesses} | array of m macro-fiber thicknesses|
| {Widths} | array of m macro-fiber widths |
| {Material_tags}| array of m macro-fiber nDMaterial [FSAM](https://opensees.berkeley.edu/wiki/index.php/FSAM_-_2D_RC_Panel_Constitutive_Behavior) tags|
| c | location of center of rotation from the base (optional, default = 0.4 (recommended))|
| tMod	| thickness modifier for out-of-plane bending behavior (optional; default = 0.63, which is equivalent to 25% of uncracked stiffness)|
| Nu | Poisson ratio for out-of-plane bending (optional, default = 0.25)|
| Dens | element density (optional, default = 0.00)|

### Recorders

The following recorders are available with the SFI-MVLEM-3D element.

| recorder | description |
|----------|------------|
| globalForce | Element global forces|
| Curvature | Element curvature|
| ShearDef | Element shear deformation|
| RCPanel $fibTag $Response | Returns RC panel (macro-fiber) $Response for a $fibTag-th panel (1 ≤ fibTag ≤ m). For available $Response-s refer to nDMaterial [FSAM](https://opensees.berkeley.edu/wiki/index.php/FSAM_-_2D_RC_Panel_Constitutive_Behavior) |

## Example

Specimen TUB (Beyer et al. 2008) is analyzed using the SFI-MVLEM-3D. Figure 2a shows the photo of the test specimen and the multidirectional displacement pattern applied at the top of the wall, while Figure 2b-c show the SFI-MVLEM-3D model of specimen TUB.

![TUB](https://user-images.githubusercontent.com/53920372/94061732-a009a900-fd9a-11ea-8d28-2ae4981326f6.JPG)
**Figure 2: SFI-MVLEM-3D Model of specimen TUB**

Figure 3 compares experimentally measured and analytically predicted load deformation behavior of the specimen TUB in E-W, N-S, and diagonal loading directions. The model provides accurate predictions of the lateral load capacity and the stiffness under cyclic loading in loading directions parallel to the principal axes of the cross-section (E-W, N-S direction). Analysis results overestimate the lateral load capacity in diagonal loading directions due to plane-sections-remain-plane assumption implemented in the model formulation that cannot capture pronounced shear lag effect observed in the test specimen.

![TUB_SFI_MVLEM_3D](https://user-images.githubusercontent.com/53920372/110193323-287b8380-7de8-11eb-8202-f557befac055.JPG)
**Figure 3: Experimental vs. SFI-MVLEM-3D load-deforamtion response of specimen TUB**

## References
K. Kolozvari, K. Kalbasi, K. Orakcal & J. W. Wallace (under review), "Three-dimensional shear-flexure interaction model for analysis of non-planar reinforced concrete walls", Journal of Building Engineering.<br/>
K. Kolozvari, K. Kalbasi, K. Orakcal, L. M. Massone & J. W. Wallace (2019), "Shear–flexure-interaction models for planar and flanged reinforced concrete walls", Bulletin of Eathquake Engineering, 17, pages 6391–6417. [link](https://link.springer.com/article/10.1007/s10518-019-00658-5)
