https://openmx-square.org/

Release note: Oct. 17, 2021

***** How to apply the patch3.9.9: *****

cp ./patch3.9.9.tar.gz openmx3.9/source
cd openmx3.9/source
tar zxvf patch3.9.9.tar.gz
mv kpoint.in ../work/
*** edit makefile, since makefile is overwritten by the patch. ***
make clean
make all
make install

***** patch3.9.9.tar.gz *****
contains 

Allocate_Arrays.c                 Eigen_lapack.c                    Set_Vpot.c                 truncation.c
Band_DFT_Col.c                    Force.c                           Set_XC_Grid.c              init.c
Band_DFT_Col_NEGF.c               Free_Arrays.c                     Set_XC_NL1_Grid.c          iterout.c
Band_DFT_Col_Optical_ScaLAPACK.c  Hamiltonian_Cluster_Hs.c          TRAN_Apply_Bias2e.c        jx_band_indiv.c
Band_DFT_Dosout.c                 Initial_CntCoes.c                 TRAN_Band_Col.c            jx_band_psum.c
Band_DFT_MO.c                     Initial_CntCoes2.c                TRAN_CDen_Main.c           jx_cluster.c
Band_DFT_NonCol.c                 Input_std.c                       TRAN_Calc_CentGreen.c      kpoint.in
Band_DFT_NonCol_GB.c              Inputtools.c                      TRAN_Calc_SurfGreen.c      makefile
Band_DFT_NonCol_Optical.c         MD_pac.c                          TRAN_Channel_Output.c      md2axsf.c
Band_DFT_kpath.c                  Make_InputFile_with_FinalCoord.c  TRAN_DFT.c                 neb.c
Band_DFT_kpath_LNO.c              Memory_Leak_test.c                TRAN_DFT_Dosout.c          neb_check.c
Calc_optical.c                    Mixing_V.c                        TRAN_Input_std.c           openmx.c
Cluster_DFT_Col.c                 Opt_Contraction.c                 TRAN_Input_std_Atoms.c     openmx_common.c
Cluster_DFT_NonCol.c              Overlap_Cluster_Ss.c              TRAN_Main_Analysis.c       openmx_common.h
Cluster_DFT_Optical.c             Poisson.c                         TRAN_Main_Analysis_NC.c    polB.c
Cluster_DFT_Optical_ScaLAPACK.c   SCF2File.c                        TRAN_Output_Trans_HS.c     readfile.c
DFT.c                             SetPara_DFT.c                     TRAN_Poisson.c             spectra.c
DFTDvdW_init.c                    Set_Allocate_Atom2CPU.c           TRAN_Set_CentOverlap.c     tp.c
DIIS_Mixing_Rhok.c                Set_Density_Grid.c                TRAN_Set_CentOverlap_NC.c  tran_prototypes.h
DosMain.c                         Set_Hamiltonian.c                 TRAN_Set_Electrode_Grid.c  tran_variables.h
EigenBand_lapack.c                Set_OLP_Kin.c                     Total_Energy.c             MulPOnly.c
Occupation_Number_LDA_U.c         TRAN_Add_Density_Lead.c           neb_run.c                  DFTD3vdW_init.c
init_alloc_first.c
elpa-2018.05.001/elpa1_merge_systems_real_template.F90
elpa-2018.05.001/elpa_solve_evp_real_2stage_double_impl.F90
elpa-2018.05.001/elpa_solve_evp_complex_2stage_double_impl.F90

***** purpose of patch3.9.9.tar.gz *****

Related to Band_DFT_Dosout.c:
When a narrow energy range is specified by Dos.Erange for a large-scale system, 
some of states can be missed. The bug will be fixed by applying the patch. 

Related to DFT.c:
In the NEGF calculations, sometimes the SCF convergence tends to get stuck. 
The problem can be reduced by applying the patch. 

Related to Make_InputFile_with_FinalCoord.c:
The directory where 'dat#' file is saved is changed to a directory specified by 
the keyword 'System.CurrrentDirectory'. The header of geometry optimization is attached
when restarting is performed without the SD file. 

Related to the execution of MulPOnly:
The sample of kpoint.in was missing in the release of OpenMX Ver. 3.9. 
Please use kpoint.in stored in the patch. 

Related to MulPOnly.c:
A MPI related bug was fixed. The bug will be fixed by applying the patch. 

Related to Occupation_Number_LDA_U.c:
The constraint schemes such as applying Zeeman terms may not work properly. 
The bug will be fixed by applying the patch. 

Related to TRAN_Add_Density_Lead.c:
For a function call of Density_Grid_Copy_B2D, the argument was improperly set. 
The bug will be fixed by applying the patch. 

Related to neb.c and neb_run.c:
For MD.NEB.Parallel.Number=1, the standard output is duplicated. 
In restarting the NEB calculation, the unit conversion of atomic coordinates were improper 
for AU and fractional cases.
The bug will be fixed by applying the patch. 

Related to openmx_common.c:
In some high symmetric structures, the forces on atoms are improperly calculated. 
The bug will be fixed by applying the patch. 

Related to openmx_common.h:
The version information is updated. 

Related to TRAN_Apply_Bias2e.c, TRAN_Band_Col.c, TRAN_CDen_Main.c, TRAN_Calc_CentGreen.c,
TRAN_Calc_SurfGreen.c, TRAN_Channel_Output.c, TRAN_DFT.c, TRAN_DFT_Dosout.c, TRAN_Input_std.c, 
TRAN_Input_std_Atoms.c, TRAN_Main_Analysis.c, TRAN_Main_Analysis_NC.c, TRAN_Output_Trans_HS.c, 
TRAN_Poisson.c, TRAN_Set_CentOverlap.c, TRAN_Set_CentOverlap_NC.c, TRAN_Set_Electrode_Grid.c:
The SCF convergence in the NEGF calculation was improved. 

Related to Force.c:
The openmp parallelization in Force3() was modified. 

Related to Total_Energy.c:
A couple of bugs in DFT-D2 and DFT-D3 methods were fixed.

Related to Band_DFT_*.c:
Determination of the number of states to be calculated was changed. 

Related to DFTDvdW_init.c and DFT3DvdW_init.c: 
Variable cell optimizations are supported. 

Related to init_alloc_first.c:
The setting is made for variables used in DFTDvdW_init.c and DFT3DvdW_init.c

Related to Cluster_DFT_Col.c:
The calculation of the partial charge was not properly performed when only the Gamma point is employed. 
The bug has been fixed by applying the patch. 

Related to makefile: 
A comiler option '-lm' is added for MulPOnly.

Related to 
elpa-2018.05.001/elpa1_merge_systems_real_template.F90
elpa-2018.05.001/elpa_solve_evp_real_2stage_double_impl.F90
elpa-2018.05.001/elpa_solve_evp_complex_2stage_double_impl.F90:
A part for the hybrid parallelization was modified. 

Related to DosMain.c:
An automatic determination of the number of meshes for energy is suppoted.

Typos in comment lines were corrected in 
Opt_Contraction.c, Initial_CntCoes.c, Initial_CntCoes2.c, jx_band_indiv.c, 
jx_band_psum.c, jx_cluster.c.

For other routines, several modifications were made to stabilize calculations, 
and known bugs reported in the OpenMX Forum were fixed. 
 