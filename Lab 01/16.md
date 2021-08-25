# Radiometric Resolution

*Add explanation of radiometric resolution, an image may be useful*

Radiometric resolution is determined from the minimum radiance to which the detector is sensitive (*L**min*), the maximum radiance at which the sensor saturates (*L**max*), and the number of bits used to store the DNs (*Q*): 

Radiometric resolution = (*L**max* - *L**min*)/2*Q*.

 It might be possible to dig around in the metadata to find values for *L**min* and *L**max*, but computing radiometric resolution is generally not necessary unless you're studying phenomena that are distinguished by very subtle changes in radiance.

