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

### installing DCM:
   You need to have an access to `ige-meom-cal1.u-ga.fr`

```
    cd $DEVGIT
    git clone ssh://<USER>@ige-meom-cal1.u-ga.fr/mnt/SSD/molines/GITSERVER/NEMODRAK_release-3.6.git
```
  See how to set up DCM in your environnement on this [documentation](DCM_getting_started.md)

### Create your MEDWEST60 configuration



## History of MEDWEST60 preparation:
### Geographical domain: Bathymetry and coordinates.

### Domain decomposition

### Initial conditions

### Open Boundaries

### 
