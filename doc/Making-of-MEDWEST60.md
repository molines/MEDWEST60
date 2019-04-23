# Making MEDWEST60 configuration

## Installing the NEMO code for this configuration
  This config share the same code as the eNATL60 experiment performed within PRACE Resumption project achieved at BSC on `marenostrum4` super computer, by Laurent Brodeau.  
  It is based on :
   * NEMO release 3-6 @rev 10404
   * XIOS 2.0  @ rev 1630
   * DCM at NEMODRAK/release-3.6 

### Good practices when using DCM (and other goodies ... )
   * assume svn repositories are in `$WORKDIR/DEV` aka `$DEVDIR`
   * assume git repositories are in `$WORKDIR/DEVGIT` aka `$DEVGIT`

### Installing DCM:
   You need to have an access to `ige-meom-cal1.u-ga.fr`

```
    cd $DEVGIT
    git clone ssh://<USER>@ige-meom-cal1.u-ga.fr/mnt/SSD/molines/GITSERVER/NEMODRAK_release-3.6.git
```
  See how to set up DCM in your environnement on this [documentation](DCM_getting_started.md)

### Create your MEDWEST60 configuration



## History of MEDWEST60 preparation:
### Geographical domain: Bathymetry and coordinates.
   * Domain : we extract the MEDWEST60 domain from eNATL60 domain using the following ncks command

   ```
       ncks -d x,5529,6409 -d y,1869,2671 eNATL60_coordinates_v3.nc4 MEDWEST60_coordinates_v1.nc
   ```

   * Bathymetry v1 is obtained with the following :

   ```
      ncks -d x,5529,6409 -d y,1869,2671  eNATL60_BATHY_GEBCO_2014_2D_msk_v3_merg.nc4 MEDWEST60_Bathymetry_v1.nc
   ```

      * Then the Bay of Biscay has been filled up using `cdfbathy` tool (as well as some points, east of Corsica where the Eastern Open boundary lays). This produced the version `v1.1`.  

### Domain decomposition
   *  This configuration is developped for running a small ensemble (10 to 20 members) at IDRIS center, on the `ada` machine (where the biggest class allows for 2048 cores).  
      Using `MPP_PREP` tool, we obtain possible  domain decomposition, first for a single member affording 2000 cores, and then for a 10 members run (each member on 200 cores) or 20 members run (each member on 100 cores).

 
   ```
     jpni  jpnj   jpi   jpj  jpi x jpj  proc  elim   sup
     -----------------------------------------------------
      51    84    20    12        240  2000  2284  0.67850
     121    34    10    26        260  2000  2114  0.73504
     
      10    37    90    24       2160   200   170  0.61065
      26    14    36    60       2160   200   164  0.61065
     
       9    20   100    43       4300   100    80  0.60782
      27     6    35   136       4760   100    62  0.67285
   ```

### Initial conditions
   * This point is to be discussed : Starting from TS fields from eNATL60 seems OK but :
      * At which date ?
      * With which level of smoothing (hourly average, daily average, monthly average ?)
      * Still a cold start with U and V set to 0. ?
      * Using a restart extraction ??

### Open Boundaries
   * Likely eNATL60 hourly data for T S U V and SSH.
     * Western BDY is located at the Gibraltar Strait, the Eastern BDT across Corsica and Sardegna.  
     * extract the mesh_mask for the boundaries (with a rim of 10 ?) and use Sosie3 for building the boundaries from eNATL60 files.  
   * Tides at the boundaries comes from the eNATL60 SSH and velocities (no harmonic constituents at the boundaries, but tidal potential ON).

### Forcing and Runoff:
   * eNATL60 was forced by DFS5.2 fields (EraInterim grid).
   * ERA5 fields may be of interest as they offer hourly atmosphere on a 1/4 deg grid.
   * Runoff : no reasons to take something different that eNATL60.

## First run 
### Prepare namelist

### Setup `includefile.ksh`

### Discuss XIOS issues

## Preparing the Ensemble code:
