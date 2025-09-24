# HXDeng-TRSM
The Quantum Espresso (QE) program with the transfer to realistic state model (TRSM) incorporated

Parameters for TRSM calculations:
&control
calculation：
calculation     = 'scf’,
prefix          = ‘XXX’,
Outdir         = ‘./‘,
restart_mode    = 'from_scratch’,
pseudo_dir      = ‘XXX’,
cal_def = .true.            
!   Default = .False. If True, do the TRSM calculation
io_chg_host = 'write’       
!   'write|read’ , write or read the wavefunction of the targeted level
ik_host_state = N1        
!   integer, N1th K point will be written; only effective when io_chg_host = 'write'
ik_def_state  = N2            
!   integer, N2th K point will be replaced (read); only effective when io_chg_host ='read’
ibnd_host_state = N3      
!   integer, N3th level will be written; only effective when io_chg_host = 'write'
ibnd_def_state  = N4       
!   integer, N4th level will be replaced (read); only effective when io_chg_host = ‘read'
iter_def_start =  N5         
!    integer, the number of scf steps after which the TRSM calculation begins
lambda_chg = q               
!    integer, the defect charge state

Work Flow:
1.	Derive the host wavefunction: 
cal_def = .true.
io_chg_host = 'write' 
    ik_host_state = 1
ibnd_host_state = N3
iter_def_start = N5
2.	Copy the chg_host folder to the directory where TRSM calculation proceeds
3.	Replace the perturbed wavefunction: 
cal_def = .true.
io_chg_host = 'read' 
    ik_def_state  = 1
    ibnd_def_state  = N4
iter_def_start = N5
lambda_chg = q

&system 
    occupations     = 'from_input'
……
OCCUPATIONS
2 2 2 2 2 2 2 2
2 2 2 2 2 2 2 2
2 2 2 2 2 2 2 2
……
……
2 2 2 2 2 2 2 2
1 0 0 0 0 0 0 0
…..
….
0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0

In each subdirectory:
./host: Calculation of the host structure     
./defect: Calculation of the neutral defect
./JM:   Calculation of the charged defect under Jellium model
./TEM:  Calculation of the charged defect under TRSM
