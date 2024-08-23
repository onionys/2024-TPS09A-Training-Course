# FourC Command List

## counting command 

    > ct 
    > ct 10

monitor mode 

    > ct -50000

## move motor

    > umv <motor_name> <angle or mm>
    > umv tth 10

## show & set motor position

show motor position in detail

    > wm <motor_name>
    > wm tth

         Two Theta
               tth
    User
     High     180.6640
     Current   32.9780
     Low     -179.3360
    Dial
     High     180.0000
     Current   32.3140
     Low     -180.0000

set motor position

    > set <motor_name> <value>
    > set tth 32

    Fri Aug 23 11:10:01 2024.  tth reset from 32.978 to 32.


set motor move range 

    > set_lm <motor_name> <min_limit> <max_limit>
    > set_lm tth -5 95

    Two Theta limits set to -5 95 (user), -4.686 95.314 (dial).

## scan motor

dscan : relative position scan

    > dscan <motor_name> <relative_start> <relative_end> <intervals> <time>
    > dscan tth -1  1               20   1

dscan multiple motors at the same time:

    > dscan tth -1  1  th -0.5 0.5  20   1

ascan : absolute position scan:

    > ascan <motor_name> <start> <end> <intervals> <time>
    > ascan tth  10 20              200  1.5

ascan multiple motors at the same time:

    > ascan tth  10 20 th  5   10   200  1.5

mesh : 2-D scan, absolute position input 

    > mesh  <motor_name> <start> <end> <intervals> <motor_name> <start> <end> <intervals> <time>
    > mesh  phi 10 45  40 chi -30 -45  40  1  

## Commonly used motor names

    TPS09A         In-House      作用
    -------------------------------
    tth            tth
    th             th
    chi            chi
    phi            phi

    phiz           str           sample height
    ftx                          sample x shift
    fty                          sample y shift
    farcx                        sample tilt angle (phi at 90, 270)
    farcy                        sample tilt angle (phi at 0, 180)

    xtran                        cryostat sample x shift
    ytran                        cryostat sample y shift
    ztran                        cryostat sample height



# Reciprocal Space Mapping Command List

## show current lattice constant and diffraction plane position

```
    > pa

    Four-Circle Geometry, Omega equals zero (mode 0)
    Sector 0
    
      Primary Reflection (at lambda 1.54):
              tth th chi phi = 60 30 0 0
                       H K L = 1 0 0
    
      Secondary Reflection (at lambda 1.54):
              tth th chi phi = 60 30 0 -90
                       H K L = 0 1 0
    
      Lattice Constants (lengths / angles):
                  real space = 1.54 1.54 1.54 / 90 90 90
            reciprocal space = 4.08 4.08 4.08 / 90 90 90
    
      Azimuthal Reference:
                       H K L = 0 0 1
    
                      Lambda = 1.54
    
     Cut Points:
          tth   th  chi  phi
         -180 -180 -180 -180
```

## set lattice constant

    > set_lat 

## set primary reflection vector

    > or0 <H> <K> <L>

    > setor0

## set secondary reflection vector

    > or1 <H> <K> <L>

    > setor1
  
## Reciprocal Space Calculation

calculate motor positions (`tth` `th` `chi` `phi`)
for specific reciprocal space vector (`H` `K` `L`)

    > ca <H> <K> <L>


calculate reciprocal space vector (`H` `K` `L`) from motor positions

    > ci <tth> <th> <chi> <phi>

### set mode

normal mode, keep tth/th to 2/1

    > unfreeze
    > setmode 0

phi fix mode, keep phi to specific value 

    > setmode 3
    > freeze <phi_value>

set sector, depending on the result of `chi` calculation

    > setsector 0
    > setsector 4

## Reciprocal Space Motor Operation

move motors to specific reciprocal space vector

    > ubr <H> <K> <L>

scan along reciprocal space axis H-axis, K-axis, and L-axis

    > hscan <H start> <H end> <steps> <time>
    > kscan <K start> <K end> <steps> <time>
    > lscan <L start> <L end> <steps> <time>

scan from (H start, K start, L start) to (H end, K end, L end) in 3D Reciprocal space

    > hklscan <H start> <H end> <K start> <K end> <L start> <L end> <steps> <time>

mesh scan in H-K plane, H-L plane, and K-L plane

    > hklmesh H <H start> <H end> <H steps> K <K start> <K end> <K steps> <time>
    > hklmesh H <H start> <H end> <H steps> L <L start> <L end> <L steps> <time>
    > hklmesh K <K start> <K end> <K steps> L <L start> <L end> <L steps> <time>

