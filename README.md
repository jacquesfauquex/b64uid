# b64uid
shrinked same-order url-safe ascii codification for unique identificators, with special consideration of DICOM ones

## use case

The DICOM identificator UID, made of numbers and dots is key for objects classification. But since it may be quite large, up to 64 chars, it results inefficient when used as file or dir name. Especially so, when subject to sorting or filter operations.

The OID encoding of UID is not efficient since it uses merely 11 codes ( 0 1 2 3 4 5 6 7 8 9 . ) out of the 256 available in each char.

b64uid aims at shrinking them, but cleverly. In particular, it complies with the following requirements:
- the result must be readable ascii
- the result must be url-safe
- the sorting of OIDs before and after shrinkage is unchanged
- the algorithm to shrink and expand should be simple and without dependencies to extern libraries

## algorithm

- map codes to half bytes

|---|---|
| half byte | code |
|---|---|
