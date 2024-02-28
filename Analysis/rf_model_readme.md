#### my_random_forest_1
- for curb extraction, only consider lower half of images
- 4 groups:
  - curb, infrastructure, other, vegetation
- Variables 29:
  - gmedian, rmedian, bmedian, gmean, rmean, bmean, gstd, rstd, bstd, gq25, gq75, rq25, rq75, bq25, bq75, cdmean, cdstd
  - area, aspect_ratio_wh_s, extent_s, solidity, aspect_ratio_wh, extent, orien_rre, orien_ell, ed, ratio_ell, perimeter, bottomm


#### my_random_forest_2_whole7
- for entropy calculation of whole scene
- 7 groups: 
  - building, curb, infrastructure, means_of_transportation, other, sky, vegetation
- Variables 32:
  - gmedian, rmedian, bmedian, gmean, rmean, bmean, gstd, rstd, bstd, gq25, gq75, rq25, rq75, bq25, bq75, cdmean, cdstd
  - area, aspect_ratio_wh_s, extent_s, solidity, aspect_ratio_wh, extent, orien_rre, orien_ell, ed, ratio_ell, perimeter, leftm, rightm, topm, bottomm



#### my_random_forest_3_ground7
- for entropy calculation of ground scene
- 7 groups: 
  - 0 bike_lane, 1 curb, 2 ground_sign, 3 manhole, 4 other, 5 pavement, 6 road
- Variables 32:
  - gmedian, rmedian, bmedian, gmean, rmean, bmean, gstd, rstd, bstd, gq25, gq75, rq25, rq75, bq25, bq75, cdmean, cdstd
  - area, aspect_ratio_wh_s, extent_s, solidity, aspect_ratio_wh, extent, orien_rre, orien_ell, ed, ratio_ell, perimeter, leftm, rightm, topm, bottomm
