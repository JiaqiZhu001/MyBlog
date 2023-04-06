---
title: Data science with Fastfood
author: Package Build
date: '2023-04-06'
slug: []
categories:
  - R
tags:
  - R Markdown
authors: []
description: ''
externalLink: ''
series: []
---

# Data science in Fast food

In this post we have dataset of fastfood item.


```r
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.1     ✔ readr     2.1.4
## ✔ forcats   1.0.0     ✔ stringr   1.5.0
## ✔ ggplot2   3.4.1     ✔ tibble    3.2.1
## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
## ✔ purrr     1.0.1     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the ]8;;http://conflicted.r-lib.org/conflicted package]8;; to force all conflicts to become errors
```

```r
library("tidymodels")
```

```
## ── Attaching packages ────────────────────────────────────── tidymodels 1.0.0 ──
## ✔ broom        1.0.4     ✔ rsample      1.1.1
## ✔ dials        1.1.0     ✔ tune         1.0.1
## ✔ infer        1.0.4     ✔ workflows    1.1.3
## ✔ modeldata    1.1.0     ✔ workflowsets 1.0.0
## ✔ parsnip      1.0.4     ✔ yardstick    1.1.0
## ✔ recipes      1.0.5     
## ── Conflicts ───────────────────────────────────────── tidymodels_conflicts() ──
## ✖ scales::discard() masks purrr::discard()
## ✖ dplyr::filter()   masks stats::filter()
## ✖ recipes::fixed()  masks stringr::fixed()
## ✖ dplyr::lag()      masks stats::lag()
## ✖ yardstick::spec() masks readr::spec()
## ✖ recipes::step()   masks stats::step()
## • Search for functions across packages at https://www.tidymodels.org/find/
```

```r
data<-read.csv("fastfood.csv")
data
```

```
##      restaurant                                                            item
## 1     Mcdonalds                                Artisan Grilled Chicken Sandwich
## 2     Mcdonalds                                  Single Bacon Smokehouse Burger
## 3     Mcdonalds                                  Double Bacon Smokehouse Burger
## 4     Mcdonalds                       Grilled Bacon Smokehouse Chicken Sandwich
## 5     Mcdonalds                        Crispy Bacon Smokehouse Chicken Sandwich
## 6     Mcdonalds                                                         Big Mac
## 7     Mcdonalds                                                    Cheeseburger
## 8     Mcdonalds                                        Classic Chicken Sandwich
## 9     Mcdonalds                                             Double Cheeseburger
## 10    Mcdonalds                             Double Quarter Pounder® with Cheese
## 11    Mcdonalds                                                   Filet-O-Fish®
## 12    Mcdonalds                                     Garlic White Cheddar Burger
## 13    Mcdonalds                   Grilled Garlic White Cheddar Chicken Sandwich
## 14    Mcdonalds                    Crispy Garlic White Cheddar Chicken Sandwich
## 15    Mcdonalds                                                       Hamburger
## 16    Mcdonalds                                                    Lobster Roll
## 17    Mcdonalds                                 Maple Bacon Dijon 1/4 lb Burger
## 18    Mcdonalds                      Grilled Maple Bacon Dijon Chicken Sandwich
## 19    Mcdonalds                       Crispy Maple Bacon Dijon Chicken Sandwich
## 20    Mcdonalds                                                       McChicken
## 21    Mcdonalds                                                        McDouble
## 22    Mcdonalds                                                           McRib
## 23    Mcdonalds                                    Pico Guacamole 1/4 lb Burger
## 24    Mcdonalds                         Grilled Pico Guacamole Chicken Sandwich
## 25    Mcdonalds                          Crispy Pico Guacamole Chicken Sandwich
## 26    Mcdonalds               Premium Buttermilk Crispy Chicken Deluxe Sandwich
## 27    Mcdonalds                          Premium Crispy Chicken Deluxe Sandwich
## 28    Mcdonalds                                    Quarter Pounder® with Cheese
## 29    Mcdonalds                                       Signature Sriracha Burger
## 30    Mcdonalds                     Grilled Signature Sriracha Chicken Sandwich
## 31    Mcdonalds                      Crispy Signature Sriracha Chicken Sandwich
## 32    Mcdonalds                                   Sweet BBQ Bacon 1/4 lb Burger
## 33    Mcdonalds                        Grilled Sweet BBQ Bacon Chicken Sandwich
## 34    Mcdonalds                         Crispy Sweet BBQ Bacon Chicken Sandwich
## 35    Mcdonalds                       3 piece Buttermilk Crispy Chicken Tenders
## 36    Mcdonalds                       4 piece Buttermilk Crispy Chicken Tenders
## 37    Mcdonalds                       6 piece Buttermilk Crispy Chicken Tenders
## 38    Mcdonalds                      10 piece Buttermilk Crispy Chicken Tenders
## 39    Mcdonalds                      12 piece Buttermilk Crispy Chicken Tenders
## 40    Mcdonalds                      20 piece Buttermilk Crispy Chicken Tenders
## 41    Mcdonalds                                       4 Piece Chicken McNuggets
## 42    Mcdonalds                                       6 Piece Chicken McNuggets
## 43    Mcdonalds                                      10 Piece Chicken McNuggets
## 44    Mcdonalds                                      20 Piece Chicken McNuggets
## 45    Mcdonalds                                      40 piece Chicken McNuggets
## 46    Mcdonalds                 4 piece Sweet N' Spicy Honey BBQ Glazed Tenders
## 47    Mcdonalds                 6 piece Sweet N' Spicy Honey BBQ Glazed Tenders
## 48    Mcdonalds                10 piece Sweet N' Spicy Honey BBQ Glazed Tenders
## 49    Mcdonalds                                 Premium Asian Salad w/o Chicken
## 50    Mcdonalds                          Premium Asian Salad w/ Grilled Chicken
## 51    Mcdonalds                           Premium Asian Salad w/ Crispy Chicken
## 52    Mcdonalds                           Premium Bacon Ranch Salad w/o Chicken
## 53    Mcdonalds                    Premium Bacon Ranch Salad w/ Grilled Chicken
## 54    Mcdonalds                     Premium Bacon Ranch Salad w/ Crispy Chicken
## 55    Mcdonalds                             Premium Southwest Salad w/o Chicken
## 56    Mcdonalds                      Premium Southwest Salad w/ Grilled Chicken
## 57    Mcdonalds                       Premium Southwest Salad w/ Crispy Chicken
## 58  Chick Fil-A                               Chargrilled Chicken Club Sandwich
## 59  Chick Fil-A                                    Chargrilled Chicken Sandwich
## 60  Chick Fil-A                                                  Chick-n-Slider
## 61  Chick Fil-A                                          1 Piece Chick-n-Strips
## 62  Chick Fil-A                                          2 Piece Chick-n-Strips
## 63  Chick Fil-A                                          3 Piece Chick-n-Strips
## 64  Chick Fil-A                                          4 piece Chick-n-Strips
## 65  Chick Fil-A                                                  Chicken Deluxe
## 66  Chick Fil-A                                         4 piece Chicken Nuggets
## 67  Chick Fil-A                                         6 piece Chicken Nuggets
## 68  Chick Fil-A                                         8 piece Chicken Nuggets
## 69  Chick Fil-A                                        12 piece Chicken Nuggets
## 70  Chick Fil-A                                        30 piece Chicken Nuggets
## 71  Chick Fil-A                                          Chicken Salad Sandwich
## 72  Chick Fil-A                                                Chicken Sandwich
## 73  Chick Fil-A                                 4 Piece Grilled Chicken Nuggets
## 74  Chick Fil-A                                 6 Piece Grilled Chicken Nuggets
## 75  Chick Fil-A                                 8 piece Grilled Chicken Nuggets
## 76  Chick Fil-A                                12 Piece Grilled Chicken Nuggets
## 77  Chick Fil-A                              Spicy Grilled Chicken Sub Sandwich
## 78  Chick Fil-A                            Regular Grilled Chicken Sub Sandwich
## 79  Chick Fil-A                                   Smokehouse BBQ Bacon Sandwich
## 80  Chick Fil-A                                          Spicy Chicken Sandwich
## 81  Chick Fil-A                                                    Spicy Deluxe
## 82  Chick Fil-A                                   Chargrilled Chicken Cool Wrap
## 83  Chick Fil-A                                     Chicken Enchiladas Meal Kit
## 84  Chick Fil-A                                       Chicken Parmesan Meal Kit
## 85        Sonic                                  Hatch Green Chile Cheeseburger
## 86        Sonic                                                 Jalapeno Burger
## 87        Sonic                                                      Jr. Burger
## 88        Sonic                                          Jr. Chili Cheeseburger
## 89        Sonic                                               Jr. Deluxe Burger
## 90        Sonic                                         Jr. Deluxe Cheeseburger
## 91        Sonic                                         Jr. Double Cheeseburger
## 92        Sonic                               Sonic Bacon Cheeseburger (w/mayo)
## 93        Sonic                                         Sonic Burger W/ Mustard
## 94        Sonic                                         Sonic Burger W/ Ketchup
## 95        Sonic                                      Sonic Burger W/ Mayonnaise
## 96        Sonic                                   Sonic Cheeseburger W/ Mustard
## 97        Sonic                                   Sonic Cheeseburger W/ Ketchup
## 98        Sonic                                Sonic Cheeseburger W/ Mayonnaise
## 99        Sonic                  Super Sonic Bacon Double Cheeseburger (w/mayo)
## 100       Sonic                      Super Sonic Double Cheeseburger W/ Mustard
## 101       Sonic                      Super Sonic Double Cheeseburger W/ Ketchup
## 102       Sonic                         Super Sonic Double Cheeseburger W/ Mayo
## 103       Sonic                        Super Sonic Jalapeno Double Cheeseburger
## 104       Sonic                                        Veggie Burger W/ Ketchup
## 105       Sonic                                      Veggie Burger With Mustard
## 106       Sonic                                        Veggie Burger W/ Mustard
## 107       Sonic                     Grilled Asiago Caesar Chicken Club Sandwich
## 108       Sonic                      Crispy Asiago Caesar Chicken Club Sandwich
## 109       Sonic                                        Grilled Chicken Sandwich
## 110       Sonic                                         Crispy Chicken Sandwich
## 111       Sonic                                          Chicken Strip Sandwich
## 112       Sonic                            3 Piece Crispy Chicken Tender Dinner
## 113       Sonic                            5 Piece Crispy Chicken Tender Dinner
## 114       Sonic                                Deluxe Ultimate Chicken Sandwich
## 115       Sonic                        Buffalo Dunked Ultimate Chicken Sandwich
## 116       Sonic                Garlic Parmesan Dunked Ultimate Chicken Sandwich
## 117       Sonic                                     Small Jumbo Popcorn Chicken
## 118       Sonic                                     Large Jumbo Popcorn Chicken
## 119       Sonic                               Small Spicy Jumbo Popcorn Chicken
## 120       Sonic                               Large Spicy Jumbo Popcorn Chicken
## 121       Sonic                       3 Piece Super Crunch Chicken Strip Dinner
## 122       Sonic                       4 Piece Super Crunch Chicken Strip Dinner
## 123       Sonic                       5 Piece Super Crunch Chicken Strip Dinner
## 124       Sonic                             3 Piece Super Crunch Chicken Strips
## 125       Sonic                             4 Piece Super Crunch Chicken Strips
## 126       Sonic                             5 Piece Super Crunch Chicken Strips
## 127       Sonic                           Traditional Ultimate Chicken Sandwich
## 128       Sonic                                           Ultimate Chicken Club
## 129       Sonic                            All Beef All-american Style Dog – 6"
## 130       Sonic                                       All Beef Chicago Dog – 6"
## 131       Sonic                                All Beef Chili Cheese Coney – 6"
## 132       Sonic                                      All Beef New York Dog – 6"
## 133       Sonic                                   All Beef Regular Hot Dog – 6"
## 134       Sonic                                Cheesy Bacon Pretzel Dog - 6 In.
## 135       Sonic                                                        Corn Dog
## 136       Sonic                                    Footlong Quarter Pound Coney
## 137       Sonic                                        The Original Pretzel Dog
## 138       Arbys                                                     Arby's Melt
## 139       Arbys                                                 Arby-Q Sandwich
## 140       Arbys                                         Beef 'n Cheddar Classic
## 141       Arbys                                             Beef 'n Cheddar Mid
## 142       Arbys                                    Bourbon BBQ Brisket Sandwich
## 143       Arbys                                    Bourbon BBQ Chicken Sandwich
## 144       Arbys                                      Bourbon BBQ Steak Sandwich
## 145       Arbys                             Buttermilk Buffalo Chicken Sandwich
## 146       Arbys                                Buttermilk Chicken Bacon & Swiss
## 147       Arbys                         Buttermilk Chicken Cordon Bleu Sandwich
## 148       Arbys                              Buttermilk Crispy Chicken Sandwich
## 149       Arbys                               Classic French Dip & Swiss/Au Jus
## 150       Arbys                                              Classic Roast Beef
## 151       Arbys                                               Double Roast Beef
## 152       Arbys                                       Fire-Roasted Philly Steak
## 153       Arbys                                               Grand Turkey Club
## 154       Arbys                                                      Greek Gyro
## 155       Arbys                             Half Pound Beef 'n Cheddar Sandwich
## 156       Arbys                                   Half Pound French Dip & Swiss
## 157       Arbys                                  Half Pound Roast Beef Sandwich
## 158       Arbys                                                Ham & Swiss Melt
## 159       Arbys                                         Loaded Italian Sandwich
## 160       Arbys                                   Pecan Chicken Salad Flatbread
## 161       Arbys                                    Pecan Chicken Salad Sandwich
## 162       Arbys                               2 piece Prime-Cut Chicken Tenders
## 163       Arbys                               3 piece Prime-Cut Chicken Tenders
## 164       Arbys                               5 piece Prime-Cut Chicken Tenders
## 165       Arbys                                                 Reuben Sandwich
## 166       Arbys                                                 Roast Beef Gyro
## 167       Arbys                                   Roast Turkey & Swiss Sandwich
## 168       Arbys                                       Roast Turkey & Swiss Wrap
## 169       Arbys                            Roast Turkey, Ranch & Bacon Sandwich
## 170       Arbys                                Roast Turkey, Ranch & Bacon Wrap
## 171       Arbys                                Smoke Mountain w/ Beef Short Rib
## 172       Arbys                              Smokehouse Beef Short Rib Sandwich
## 173       Arbys                                              Smokehouse Brisket
## 174       Arbys                                                Super Roast Beef
## 175       Arbys                                     Three Cheese Steak Sandwich
## 176       Arbys                                          Triple Decker Sandwich
## 177       Arbys                                             Turkey Avocado Club
## 178       Arbys                                                     Turkey Gyro
## 179       Arbys                                                    Ultimate BLT
## 180       Arbys                                          Buffalo Chicken Slider
## 181       Arbys                                 Chicken Tender 'n Cheese Slider
## 182       Arbys                                    Corned Beef 'n Cheese Slider
## 183       Arbys                                            Ham 'n Cheese Slider
## 184       Arbys                            Jalapeno Roast Beef 'n Cheese Slider
## 185       Arbys                                                    Pizza Slider
## 186       Arbys                                     Roast Beef 'n Cheese Slider
## 187       Arbys                                         Turkey 'n Cheese Slider
## 188       Arbys                                              Chopped Side Salad
## 189       Arbys                                  Crispy Chicken Farmhouse Salad
## 190       Arbys                                                Greek Gyro Salad
## 191       Arbys                                    Roast Turkey Farmhouse Salad
## 192       Arbys                                               Super Greek Salad
## 193 Burger King                                         American Brewhouse King
## 194 Burger King                                    Bacon & Swiss Sourdough King
## 195 Burger King                                              Bacon Cheeseburger
## 196 Burger King                                       Bacon Cheeseburger Deluxe
## 197 Burger King                                                      Bacon King
## 198 Burger King                                                   Bacon King Jr
## 199 Burger King                                                  BBQ Bacon King
## 200 Burger King                                                    Cheeseburger
## 201 Burger King                                       Double Bacon Cheeseburger
## 202 Burger King                                             Double Cheeseburger
## 203 Burger King                                                Double Hamburger
## 204 Burger King                                       Double Quarter Pound King
## 205 Burger King                                         Extra Long Cheeseburger
## 206 Burger King                                                  Farmhouse King
## 207 Burger King                                                       Hamburger
## 208 Burger King                                          Homestyle Cheeseburger
## 209 Burger King                                          Jalapeno King Sandwich
## 210 Burger King                                           Mushroom & Swiss King
## 211 Burger King                                                    Rodeo Burger
## 212 Burger King                                                      Rodeo King
## 213 Burger King                                           Sourdough King Single
## 214 Burger King                                           Sourdough King Double
## 215 Burger King                                                 Steakhouse King
## 216 Burger King                                          Bacon & Cheese Whopper
## 217 Burger King                                       DOUBLE WHOPPER w/o Cheese
## 218 Burger King                                        DOUBLE WHOPPER w/ Cheese
## 219 Burger King                                              WHOPPER w/o Cheese
## 220 Burger King                                               WHOPPER w/ Cheese
## 221 Burger King                                          WHOPPER JR. w/o Cheese
## 222 Burger King                                           WHOPPER JR. w/ Cheese
## 223 Burger King Bacon Cheddar Ranch Chicken Salad w/ grilled Chicken & Dressing
## 224 Burger King  Bacon Cheddar Ranch Chicken Salad w/ crispy Chicken & Dressing
## 225 Burger King                            Chicken BLT Salad w/ Grilled Chicken
## 226 Burger King                             Chicken BLT Salad w/ Crispy Chicken
## 227 Burger King                         Chicken Caesar Salad w/ Grilled Chicken
## 228 Burger King                          Chicken Caesar Salad w/ Crispy Chicken
## 229 Burger King             Chicken, Apple & Cranberry Salad w/ Grilled Chicken
## 230 Burger King              Chicken, Apple & Cranberry Salad w/ Crispy Chicken
## 231 Burger King    Garden Grilled Chicken Salad w/ Grilled Chicken, no dressing
## 232 Burger King     Garden Grilled Chicken Salad w/ Crispy Chicken, no dressing
## 233 Burger King                                 Side Caesar Salad with dressing
## 234 Burger King                    Side Garden Salad and Avocado Ranch Dressing
## 235 Burger King                     Bacon Cheddar Ranch Crispy Chicken Sandwich
## 236 Burger King                               BBQ Bacon Crispy Chicken Sandwich
## 237 Burger King                                               Big Fish Sandwich
## 238 Burger King                                                BK VEGGIE Burger
## 239 Burger King                                                  Chicken Burger
## 240 Burger King                                    Chicken Cordon Bleu Sandwich
## 241 Burger King                                                   Chicken Fries
## 242 Burger King                                         4 Piece Chicken Nuggets
## 243 Burger King                                         6 Piece Chicken Nuggets
## 244 Burger King                                        20 Piece Chicken Nuggets
## 245 Burger King                                          Chicken Nuggets (10pc)
## 246 Burger King                                       Chicken Parmesan Sandwich
## 247 Burger King                                     Crispy Buffalo Chicken Melt
## 248 Burger King                                              Crispy Chicken Jr.
## 249 Burger King                                         Crispy Chicken Sandwich
## 250 Burger King                                        Grilled Chicken Sandwich
## 251 Burger King                                        Grilled Chili Cheese Dog
## 252 Burger King                                                 Grilled Hot Dog
## 253 Burger King                                          Jalapeno Chicken Fries
## 254 Burger King                                       Original Chicken Sandwich
## 255 Burger King                                           Pretzel Chicken Fries
## 256 Burger King                                   Rodeo Crispy Chicken Sandwich
## 257 Burger King                                          Sourdough Chicken Club
## 258 Burger King                                   4 Piece Spicy Chicken Nuggets
## 259 Burger King                                           Spicy Chicken Nuggets
## 260 Burger King                                        Spicy Crispy Chicken Jr.
## 261 Burger King                                   Spicy Crispy Chicken Sandwich
## 262 Burger King                          Spicy Crispy Jalapeno Chicken Sandwich
## 263 Dairy Queen                               1/2 lb. FlameThrower® GrillBurger
## 264 Dairy Queen                                 1/2 lb. GrillBurger with Cheese
## 265 Dairy Queen                                1/4 lb. Bacon Cheese GrillBurger
## 266 Dairy Queen                                 1/4 lb. GrillBurger with Cheese
## 267 Dairy Queen                              1/4 lb. Mushroom Swiss GrillBurger
## 268 Dairy Queen                                           Original Cheeseburger
## 269 Dairy Queen                                    Original Double Cheeseburger
## 270 Dairy Queen                   4 Piece Chicken Strip Basket w/ Country Gravy
## 271 Dairy Queen                   6 Piece Chicken Strip Basket w/ Country Gravy
## 272 Dairy Queen                                                Bacon Cheese Dog
## 273 Dairy Queen                                                      Cheese Dog
## 274 Dairy Queen                                                Chili Cheese Dog
## 275 Dairy Queen                                                       Chili Dog
## 276 Dairy Queen                                                         Hot Dog
## 277 Dairy Queen                                                      Relish Dog
## 278 Dairy Queen                                          Barbecue Pork Sandwich
## 279 Dairy Queen                                               Breaded Mushrooms
## 280 Dairy Queen                                            Regular Cheese Curds
## 281 Dairy Queen                                              Large Cheese Curds
## 282 Dairy Queen                                           Chili Cheese Mega Dog
## 283 Dairy Queen                                                        Corn Dog
## 284 Dairy Queen                                            Crispy Fish Sandwich
## 285 Dairy Queen                                             Deluxe Cheeseburger
## 286 Dairy Queen                                      Deluxe Double Cheeseburger
## 287 Dairy Queen                                         Deluxe Double Hamburger
## 288 Dairy Queen                                                Deluxe Hamburger
## 289 Dairy Queen                                             DQ Ultimate® Burger
## 290 Dairy Queen                                        Pork Tenderloin Sandwich
## 291 Dairy Queen                                             Steak Finger Basket
## 292 Dairy Queen                                 3 chicken strips Chicken Strips
## 293 Dairy Queen                                    Chicken Bacon Ranch Sandwich
## 294 Dairy Queen                                     Chicken Mozzarella Sandwich
## 295 Dairy Queen                                        Crispy Chicken BLT Salad
## 296 Dairy Queen                              Crispy Chicken Garden Greens Salad
## 297 Dairy Queen                                         Crispy Chicken Sandwich
## 298 Dairy Queen                                             Crispy Chicken Wrap
## 299 Dairy Queen                                       Grilled Chicken BLT Salad
## 300 Dairy Queen                             Grilled Chicken Garden Greens Salad
## 301 Dairy Queen                                        Grilled Chicken Sandwich
## 302 Dairy Queen                                            Grilled Chicken Wrap
## 303 Dairy Queen                                                      Side Salad
## 304 Dairy Queen                                             Turkey BLT Sandwich
## 305      Subway                                                       6" B.L.T.
## 306      Subway                                                 Footlong B.L.T.
## 307      Subway                                             6" BBQ Rib Sandwich
## 308      Subway                                       Footlong BBQ Rib Sandwich
## 309      Subway                                             6" Big Hot Pastrami
## 310      Subway                                       Footlong Big Hot Pastrami
## 311      Subway                                       6" Big Philly Cheesesteak
## 312      Subway                                 Footlong Big Philly Cheesesteak
## 313      Subway                                  Kids Mini Sub Black Forest Ham
## 314      Subway                                             6" Black Forest Ham
## 315      Subway                                       Footlong Black Forest Ham
## 316      Subway                                                6" Carved Turkey
## 317      Subway                                          Footlong Carved Turkey
## 318      Subway                              6" Carved Turkey & Bacon w/ Cheese
## 319      Subway                        Footlong Carved Turkey & Bacon w/ Cheese
## 320      Subway                                   6" Chicken & Bacon Ranch Melt
## 321      Subway                             Footlong Chicken & Bacon Ranch Melt
## 322      Subway                                        6" Chicken Pizziola Melt
## 323      Subway                                  Footlong Chicken Pizziola Melt
## 324      Subway                                               6" Cold Cut Combo
## 325      Subway                                         Footlong Cold Cut Combo
## 326      Subway                                           6" Corned Beef Reuben
## 327      Subway                                     Footlong Corned Beef Reuben
## 328      Subway                                               6" Italian B.M.T.
## 329      Subway                                         Footlong Italian B.M.T.
## 330      Subway                                                 6" Italian Hero
## 331      Subway                                           Footlong Italian Hero
## 332      Subway                                            6" Meatball Marinara
## 333      Subway                                      Footlong Meatball Marinara
## 334      Subway                                         6" Oven Roasted Chicken
## 335      Subway                                   Footlong Oven Roasted Chicken
## 336      Subway                                        Kids Mini Sub Roast Beef
## 337      Subway                                                   6" Roast Beef
## 338      Subway                                             Footlong Roast Beef
## 339      Subway                                     6" Rotisserie Style Chicken
## 340      Subway                               Footlong Rotisserie Style Chicken
## 341      Subway                                                6" Spicy Italian
## 342      Subway                                          Footlong Spicy Italian
## 343      Subway                                             6" Steak and Cheese
## 344      Subway                                       Footlong Steak and Cheese
## 345      Subway                                                  6" Subway Club
## 346      Subway                                            Footlong Subway Club
## 347      Subway                                6" Subway Melt (includes cheese)
## 348      Subway                          Footlong Subway Melt (includes cheese)
## 349      Subway                                     6" Subway Seafood Sensation
## 350      Subway                               Footlong Subway Seafood Sensation
## 351      Subway                                 6" Sweet Onion Chicken Teriyaki
## 352      Subway                           Footlong Sweet Onion Chicken Teriyaki
## 353      Subway                                                         6" Tuna
## 354      Subway                                                   Footlong Tuna
## 355      Subway                                       6" Turkey & Bacon Avocado
## 356      Subway                                 Footlong Turkey & Bacon Avocado
## 357      Subway                                     Kids Mini Sub Turkey Breast
## 358      Subway                                                6" Turkey Breast
## 359      Subway                                          Footlong Turkey Breast
## 360      Subway                                          6" Turkey Breast & Ham
## 361      Subway                                    Footlong Turkey Breast & Ham
## 362      Subway                        6" Turkey Italiano Melt (with Provolone)
## 363      Subway                  Footlong Turkey Italiano Melt (with Provolone)
## 364      Subway                                     Kids Mini Sub Veggie Delite
## 365      Subway                                                6" Veggie Delite
## 366      Subway                                          Footlong Veggie Delite
## 367      Subway                                                 6" Veggie Patty
## 368      Subway                                           Footlong Veggie Patty
## 369      Subway                                      Autumn Carved Turkey Salad
## 370      Subway                                                    B.L.T. Salad
## 371      Subway                                     Big Hot Pastrami Melt Salad
## 372      Subway                                    Big Philly Cheesesteak Salad
## 373      Subway                                          Black Forest Ham Salad
## 374      Subway                     Buffalo Chicken Salad (with Ranch dressing)
## 375      Subway                           Carved Turkey & Bacon w/ Cheese Salad
## 376      Subway                                             Carved Turkey Salad
## 377      Subway      Chicken & Bacon Ranch Melt Salad (includes Ranch dressing)
## 378      Subway                                            Cold Cut Combo Salad
## 379      Subway                                            Double Chicken Salad
## 380      Subway                                           Italian B.M.T.® Salad
## 381      Subway                                              Italian Hero Salad
## 382      Subway                                         Meatball Marinara Salad
## 383      Subway                                      Oven Roasted Chicken Salad
## 384      Subway                                                Roast Beef Salad
## 385      Subway                                             Spicy Italian Salad
## 386      Subway                                            Steak & Cheese Salad
## 387      Subway                                               Subway Club Salad
## 388      Subway                                              Subway Melt® Salad
## 389      Subway                              Sweet Onion Chicken Teriyaki Salad
## 390      Subway                                                      Tuna Salad
## 391      Subway                                       Turkey Breast & Ham Salad
## 392      Subway                                             Turkey Breast Salad
## 393      Subway                                             Veggie Delite Salad
## 394      Subway                          Chipotle Southwest Steak & Cheese Wrap
## 395      Subway                            Rotisserie-Style Chicken Caesar Wrap
## 396      Subway                                  Turkey, Bacon & Guacamole Wrap
## 397      Subway                                          Cheese & Veggies Pizza
## 398      Subway                                                    Cheese Pizza
## 399      Subway                                                 Pepperoni Pizza
## 400      Subway                                                   Sausage Pizza
## 401   Taco Bell                                  1/2 lb.* Cheesy Potato Burrito
## 402   Taco Bell                                          1/2 lb.* Combo Burrito
## 403   Taco Bell                                                 7-Layer Burrito
## 404   Taco Bell                                                    Bean Burrito
## 405   Taco Bell                                           Beefy 5-Layer Burrito
## 406   Taco Bell                                           Beefy Fritos® Burrito
## 407   Taco Bell                                              Black Bean Burrito
## 408   Taco Bell                                         Burrito Supreme® – Beef
## 409   Taco Bell                                      Burrito Supreme® - Chicken
## 410   Taco Bell                                        Burrito Supreme® - Steak
## 411   Taco Bell                                 Cantina Power Burrito - Chicken
## 412   Taco Bell                                   Cantina Power Burrito - Steak
## 413   Taco Bell                                  Cantina Power Burrito - Veggie
## 414   Taco Bell                                    Cheesy Bean and Rice Burrito
## 415   Taco Bell                                            Chili Cheese Burrito
## 416   Taco Bell                             Chicken Crunchy Cheesy Core Burrito
## 417   Taco Bell                               Steak Crunchy Cheesy Core Burrito
## 418   Taco Bell                                Beef Crunchy Cheesy Core Burrito
## 419   Taco Bell                                             Loaded Taco Burrito
## 420   Taco Bell                                               Chicken Quesarito
## 421   Taco Bell                                                 Steak Quesarito
## 422   Taco Bell                                                  Beef Quesarito
## 423   Taco Bell                                        Shredded Chicken Burrito
## 424   Taco Bell                                        Smothered Burrito - Beef
## 425   Taco Bell                            Smothered Burrito - Shredded Chicken
## 426   Taco Bell                                       Smothered Burrito - Steak
## 427   Taco Bell                               Chicken Spicy Cheesy Core Burrito
## 428   Taco Bell                                 Steak Spicy Cheesy Core Burrito
## 429   Taco Bell                                  Beef Spicy Cheesy Core Burrito
## 430   Taco Bell                                             Triple Melt Burrito
## 431   Taco Bell                                XXL Grilled Stuft Burrito - Beef
## 432   Taco Bell                             XXL Grilled Stuft Burrito - Chicken
## 433   Taco Bell                               XXL Grilled Stuft Burrito - Steak
## 434   Taco Bell                                               Chicken Soft Taco
## 435   Taco Bell                        Cool Ranch® Doritos® Double Decker® Taco
## 436   Taco Bell                                 Cool Ranch® Doritos® Locos Taco
## 437   Taco Bell                         Cool Ranch® Doritos® Locos Taco Supreme
## 438   Taco Bell                                                    Crunchy Taco
## 439   Taco Bell                                           Crunchy Taco Supreme®
## 440   Taco Bell                                             Double Decker® Taco
## 441   Taco Bell                                    DOUBLE DECKER® Taco Supreme®
## 442   Taco Bell                                 Spicy Sweet Double Stacked Taco
## 443   Taco Bell                         Cool Ranch Habanero Double Stacked Taco
## 444   Taco Bell                                Nacho Crunch Double Stacked Taco
## 445   Taco Bell                              Fiery Doritos® Double Decker® Taco
## 446   Taco Bell                                       Fiery Doritos® Locos Taco
## 447   Taco Bell                               Fiery Doritos® Locos Taco Supreme
## 448   Taco Bell                                         Grilled Steak Soft Taco
## 449   Taco Bell                       Nacho Cheese Doritos® Double Decker® Taco
## 450   Taco Bell                               Nacho Cheese Doritos® Locos Tacos
## 451   Taco Bell                       Nacho Cheese Doritos® Locos Tacos Supreme
## 452   Taco Bell                                       Soft Taco Supreme® – Beef
## 453   Taco Bell                                                  Soft Taco-Beef
## 454   Taco Bell                                          Spicy Potato Soft Taco
## 455   Taco Bell                                      Chalupa Supreme® - Chicken
## 456   Taco Bell                                        Chalupa Supreme® - Steak
## 457   Taco Bell                                           Chalupa Supreme®–Beef
## 458   Taco Bell                                                  Double Chalupa
## 459   Taco Bell                                      Wild Naked Chicken Chalupa
## 460   Taco Bell                                      Mild Naked Chicken Chalupa
## 461   Taco Bell                                            Spicy Double Chalupa
## 462   Taco Bell                                             Fresco Bean Burrito
## 463   Taco Bell                               Fresco Burrito Supreme® – Chicken
## 464   Taco Bell                                 Fresco Burrito Supreme® – Steak
## 465   Taco Bell                                        Fresco Chicken Soft Taco
## 466   Taco Bell                                             Fresco Crunchy Taco
## 467   Taco Bell                                  Fresco Grilled Steak Soft Taco
## 468   Taco Bell                                                Fresco Soft Taco
## 469   Taco Bell                                           Cheesy Gordita Crunch
## 470   Taco Bell                     Doritos® Cheesy Gordita Crunch - Cool Ranch
## 471   Taco Bell                          Doritos® Cheesy Gordita Crunch - Fiery
## 472   Taco Bell                   Doritos® Cheesy Gordita Crunch - Nacho Cheese
## 473   Taco Bell                                    Double Cheesy Gordita Crunch
## 474   Taco Bell                                         Gordita Supreme® – Beef
## 475   Taco Bell                                      Gordita Supreme® - Chicken
## 476   Taco Bell                                        Gordita Supreme® - Steak
## 477   Taco Bell                                          Nacho Fries Bellgrande
## 478   Taco Bell                                              Nachos BellGrande®
## 479   Taco Bell                                                  Nachos Supreme
## 480   Taco Bell                                             Triple Layer Nachos
## 481   Taco Bell                                              Triple Melt Nachos
## 482   Taco Bell                                 Beefy Cheddar Crunchwrap Slider
## 483   Taco Bell                                           Beefy Mini Quesadilla
## 484   Taco Bell                                             Beefy Nacho Griller
## 485   Taco Bell                                           BLT Crunchwrap Slider
## 486   Taco Bell                                    Cantina Power Bowl - Chicken
## 487   Taco Bell                                      Cantina Power Bowl - Steak
## 488   Taco Bell                                     Cantina Power Bowl - Veggie
## 489   Taco Bell                                               Cheese Quesadilla
## 490   Taco Bell                                                  Cheese Roll-Up
## 491   Taco Bell                                              Chicken Quesadilla
## 492   Taco Bell                                                       Chickstar
## 493   Taco Bell                                            Chili Cheese Burrito
## 494   Taco Bell                                 Chipotle Crispy Chicken Griller
## 495   Taco Bell                                       Crispy Chicken Quesadilla
## 496   Taco Bell                                             Crunchwrap Supreme®
## 497   Taco Bell                                                  Double Tostada
## 498   Taco Bell                                     Express Taco Salad w/ Chips
## 499   Taco Bell                                           Loaded Potato Griller
## 500   Taco Bell                                                   Mexican Pizza
## 501   Taco Bell                                                       MexiMelt®
## 502   Taco Bell                                                 Steak Quesalupa
## 503   Taco Bell                                               Chicken Quesalupa
## 504   Taco Bell                                                  Beef Quesalupa
## 505   Taco Bell                                Shredded Chicken Mini Quesadilla
## 506   Taco Bell                                 Spicy Chicken Crunchwrap Slider
## 507   Taco Bell                                                   Spicy Tostada
## 508   Taco Bell                                                         Stacker
## 509   Taco Bell                                                Steak Quesadilla
## 510   Taco Bell                               Original Triple Double Crunchwrap
## 511   Taco Bell                                  Spicy Triple Double Crunchwrap
## 512   Taco Bell                                     Express Taco Salad w/ Chips
## 513   Taco Bell                                          Fiesta Taco Salad-Beef
## 514   Taco Bell                                       Fiesta Taco Salad-Chicken
## 515   Taco Bell                                         Fiesta Taco Salad-Steak
##     calories cal_fat total_fat sat_fat trans_fat cholesterol sodium total_carb
## 1        380      60         7     2.0       0.0          95   1110         44
## 2        840     410        45    17.0       1.5         130   1580         62
## 3       1130     600        67    27.0       3.0         220   1920         63
## 4        750     280        31    10.0       0.5         155   1940         62
## 5        920     410        45    12.0       0.5         120   1980         81
## 6        540     250        28    10.0       1.0          80    950         46
## 7        300     100        12     5.0       0.5          40    680         33
## 8        510     210        24     4.0       0.0          65   1040         49
## 9        430     190        21    11.0       1.0          85   1040         35
## 10       770     400        45    21.0       2.5         175   1290         42
## 11       380     170        18     4.0       0.0          40    640         38
## 12       620     300        34    13.0       1.5          95    790         48
## 13       530     180        20     7.0       0.0         125   1150         48
## 14       700     300        34     9.0       0.0          85   1190         67
## 15       250      70         8     3.0       0.0          30    480         31
## 16       290      50         5     1.5       0.0          65    630         35
## 17       640     330        36    14.0       1.5         110   1260         40
## 18       580     190        21     8.0       0.0         135   1890         50
## 19       740     310        35     9.0       0.5          95   1780         69
## 20       350     130        15     3.5       0.0          40    600         40
## 21       380     160        18     8.0       1.0          70    840         34
## 22       480     200        22     7.0       0.0          80    870         45
## 23       580     300        33    12.0       1.5          95    920         41
## 24       520     160        18     6.0       0.0         115   1540         50
## 25       680     280        32     7.0       0.0          80   1430         69
## 26       570     200        23     5.0       0.0          60   1050         64
## 27       530     200        22     4.0       0.0          45   1000         59
## 28       530     240        27    13.0       1.5         100   1090         41
## 29       670     320        35    12.0       1.5          95   1010         56
## 30       560     180        20     5.0       0.0         115   1550         56
## 31       730     300        33     7.0       0.0          80   1430         75
## 32       690     340        37    14.0       1.5         110   1310         51
## 33       630     200        22     7.0       0.0         135   1930         61
## 34       800     320        36     9.0       0.5          95   1820         80
## 35       370     190        21     3.5       0.0          70    910         16
## 36       480     250        28     4.5       0.0          95   1290         21
## 37       760     390        44     8.0       0.5         145   1890         32
## 38      1210     630        70    12.0       1.0         240   3230         52
## 39      1510     790        88    15.0       1.0         295   3770         64
## 40      2430    1270       141    24.0       2.0         475   6080        103
## 41       180     100        11     2.0       0.0          30    340         11
## 42       270     140        16     2.5       0.0          45    510         16
## 43       440     240        27     4.5       0.0          75    840         26
## 44       890     480        53     9.0       0.0         145   1680         53
## 45      1770     960       107    18.0       0.5         295   3370        105
## 46       640     240        27     4.0       0.0         105   1780         63
## 47       960     360        40     6.0       0.0         160   2670         94
## 48      1600     600        66    10.0       0.0         265   4450        156
## 49       140      70         7     0.5       0.0           0     20         13
## 50       270      80         9     1.0       0.0          80    740         18
## 51       490     250        28     8.0       0.0          95   1120         28
## 52       190     110        12     5.0       0.0          40    660          9
## 53       320     120        14     6.0       0.0          45   1230          9
## 54       490     250        28     8.0       0.0          95   1120         28
## 55       220      90        10     3.5       0.0          15    500         26
## 56       350     100        12     4.5       0.0         110   1070         27
## 57       520     230        25     6.0       0.0          75    960         46
## 58       430     144        16     8.0       0.0          85   1120         37
## 59       310      54         6     2.0       0.0          55    820         36
## 60       270      99        11     2.5       0.0          45    800         26
## 61       120      54         6     3.0       0.0          25    320          6
## 62       230     108        12     3.0       0.0          55    630         13
## 63       350     153        17     3.0       0.0          70    940         22
## 64       470     207        23     3.0       0.0          90   1250         29
## 65       500     207        23     7.0       0.0          75   1590         42
## 66       130      54         6     1.5       0.0          40    490          5
## 67       190      81         9     1.5       0.0          55    730          7
## 68       260     110        12     3.0       0.0          70    990          9
## 69       390     162        18     1.5       0.0         115   1460         14
## 70       970     414        46     2.5       0.0         285   3660         35
## 71       490     170        19     3.0       0.0          80   1130         55
## 72       440     171        19     4.0       0.0          60   1350         40
## 73        70      18         2     1.0       0.0          35    220          1
## 74       110      27         3     1.0       0.0          50    330          2
## 75       140      36         4     1.0       0.0          70    440          2
## 76       210      45         5     1.0       0.0         100    670          3
## 77       430     108        12     4.5       0.0          85   1310         47
## 78       450     117        13     6.0       0.0          75   1000         48
## 79       500     162        18     0.0       0.0          95   1200         46
## 80       450     171        19     4.0       0.0          60   1620         41
## 81       540     225        25     8.0       0.0          80   1760         43
## 82       350     126        14     5.0       0.0          60    960         29
## 83       860     423        47    16.0       1.0         100   2520         70
## 84       720     279        31    15.0       0.0         120   1780         65
## 85       710     380        43    17.0       2.0         120   1120         44
## 86       640     330        37    14.0       2.0         100    930         42
## 87       340     150        17     6.0       1.0          35    640         34
## 88       410     220        24     9.0       0.5          55    730         32
## 89       380     200        23     6.0       1.0          40    470         32
## 90       450     250        28     9.0       1.0          60    800         33
## 91       600     350        38    16.0       2.0         110   1350         35
## 92       870     530        59    20.0       2.0         140   1350         45
## 93       640     330        37    14.0       2.0         100    790         43
## 94       650     340        37    14.0       2.0         100    860         46
## 95       740     430        48    15.0       2.0         110    760         44
## 96       710     380        43    17.0       2.0         120   1120         43
## 97       720     380        43    17.0       2.0         120   1190         47
## 98       800     480        54    18.0       2.0         130   1090         44
## 99      1280     830        92    36.0       4.0         260   1630         44
## 100     1120     680        76    32.0       4.0         235   1550         44
## 101     1130     680        76    32.0       4.0         235   1620         47
## 102     1220     780        87    34.0       4.0         245   1520         45
## 103     1120     680        76    32.0       4.0         235   1690         43
## 104      450     130        14     4.0       0.0          10   1410         67
## 105      450     130        14     4.0       0.0          10   1350         64
## 106      450     130        14     4.0       0.0          10   1300         64
## 107      610     270        30     7.0       0.0         110   1570         44
## 108      680     350        39     9.0       0.0          80   1120         53
## 109      430     180        20     4.0       0.0          80    940         33
## 110      570     300        33     5.0       0.0          45   1060         47
## 111      450     220        24     4.0       0.0          35    740         43
## 112      280     130        14     2.5       0.0           0    800         16
## 113      470     220        24     4.5       0.0           0   1340         26
## 114      740     350        39     8.0       0.0          90   1550         63
## 115     1000     550        61    12.0       0.5         125   4520         70
## 116     1350     900       100    17.0       0.0         190   2180         69
## 117      380     190        22     4.0       0.0          45   1250         27
## 118      560     290        32     6.0       1.0          65   1890         41
## 119      350     150        17     3.0       0.0          45    860         30
## 120      610     270        30     5.0       0.0          80   1500         51
## 121      970     410        46     8.0       1.0          55   2160        109
## 122     1080     460        51     9.0       1.0          75   2390        118
## 123     1190     510        57    10.0       1.0          90   2610        126
## 124      330     140        16     3.0       0.0          55    670         25
## 125      440     190        21     4.0       0.0          70    900         34
## 126      550     240        26     5.0       0.0          90   1120         42
## 127      730     350        39     8.0       0.0          90   1540         62
## 128      100     580        64    15.0       0.5         100   2070         65
## 129      370     160        18     7.0       0.0          40   1180         40
## 130      430     180        20     7.0       0.0          40   2310         49
## 131      410     230        26    11.0       0.0          65   1140         30
## 132      340     170        19     7.0       0.0          40   1250         30
## 133      320     160        18     7.0       0.0          40    870         27
## 134      500     240        26    10.0       0.0          50   1410         46
## 135      210     100        11     4.0       0.0          20    530         23
## 136      830     490        54    22.0       1.0          85   1940         54
## 137      320     160        18     7.0       0.0          35    910         27
## 138      330     100        11     4.0       0.0          30    920         40
## 139      400      90        10     3.0       0.0          30   1230         58
## 140      450     180        20     6.0       1.0          50   1280         45
## 141      630     290        32    11.0       1.5         100   2100         48
## 142      650     300        33    12.0       1.0         105   1460         51
## 143      690     280        31     9.0       0.0          90   1990         66
## 144      690     280        31     9.0       0.0          90   1990         66
## 145      540     220        24     4.5       0.0          60   2110         53
## 146      650     280        31     9.0       0.0          90   1750         56
## 147      690     310        35    10.0       0.0         110   2000         53
## 148      550     230        26     4.5       0.0          60   1480         52
## 149      540     210        23    11.0       1.0          85   2500         50
## 150      360     120        14     5.0       0.5          50    970         37
## 151      510     210        24     9.0       1.5          95   1610         38
## 152      640     290        32    11.0       0.5         105   1950         46
## 153      480     220        24     7.0       0.0          65   1610         37
## 154      710     390        44    13.0       0.0          75   1360         55
## 155      740     350        39    14.0       2.0         130   2530         48
## 156      750     330        36    17.0       2.0         150   3350         51
## 157      610     270        30    12.0       2.0         130   2040         38
## 158      300      80         9     4.0       0.0          35   1030         37
## 159      680     360        40    14.0       0.5         100   2270         49
## 160      710     410        46     7.0       0.5          65    980         53
## 161      840     400        44     6.0       0.5          75   1210         81
## 162      240     100        11     1.5       0.0          30    640         19
## 163      360     150        17     2.5       0.0          45    950         28
## 164      600     250        28     4.0       0.0          75   1590         47
## 165      680     280        31     8.0       0.5          80   2420         62
## 166      550     260        29     7.0       1.0          60   1290         48
## 167      710     260        28     7.0       0.0          65   1930         79
## 168      520     240        27     9.0       0.0          65   1640         39
## 169      800     310        34    10.0       0.5          80   2420         79
## 170      620     310        34    11.0       0.5          85   2130         39
## 171      740     320        35    13.0       1.0         125   2050         62
## 172      590     250        59    10.0       1.0          75   1510         59
## 173      600     310        35    12.0       1.0         110   1240         42
## 174      430     160        17     5.0       1.0          45   1060         45
## 175      650     320        36    15.0       1.0         115   1760         44
## 176     1030     459        51    17.0       1.0         155   2940         83
## 177      730     252        28     6.0       0.0          65   2140         80
## 178      470     180        20     3.5       0.0          45   1520         48
## 179      980     495        55    14.0       0.0          85   2130         80
## 180      290     120        13     2.0       0.0          20    860         31
## 181      290     110        12     3.5       0.0          25    720         30
## 182      220      80         9     3.5       0.0          30    890         21
## 183      210      70         8     3.0       0.0          25    780         21
## 184      240      90        11     4.5       0.0          30    670         21
## 185      300     150        17     6.0       0.0          35    930         23
## 186      240      90        11     4.5       0.0          30    670         21
## 187      200      60         7     2.5       0.0          25    760         21
## 188       70      45         5     2.5       0.0          15    100          4
## 189      430     220        24     8.0       0.0          65   1000         26
## 190      420     340        37     9.0       0.0          55    700         11
## 191      230     120        13     7.0       0.0          55    870          8
## 192      720     480        53    15.0       0.0          85   1310         39
## 193     1550    1134       126    47.0       8.0         805   1820         21
## 194     1000     585        65    24.0       3.0         200   1320         48
## 195      330     140        16     7.0       0.0          55    830         32
## 196      290     120        14     6.0       0.5          40    720         28
## 197     1040     630        48    28.0       2.5         220   1900         48
## 198      730     351        39     9.0       0.0          90   1930         63
## 199     1100     675        75    29.0       3.0         220   1850         51
## 200      300     130        14     6.0       0.0          45    710         28
## 201      520     280        31    14.0       1.0         105   1180         33
## 202      450     230        26    12.0       1.0          95    960         29
## 203      360     160        18     8.0       0.0          70    520         28
## 204      900     486        54    25.0       3.0         210   1740         50
## 205      580     300        33    13.0       1.5          85   1030         45
## 206     1220     720        80    28.0       3.0         335   2050         62
## 207      260      90        10     4.0       0.0          35    490         28
## 208      550     250        27    12.0       1.5          95   1140         48
## 209      990     585        65    24.0       3.0         205   1550         46
## 210      940     567        63    21.0       2.5         175   1380         45
## 211      310     110        13     4.0       0.5          25    450         38
## 212     1250     738        82    31.0       3.5         230   2270         69
## 213      730     387        43    16.0       1.5         125   1570         52
## 214      970     549        61    24.0       3.0         205   1640         52
## 215     1100     666        74    24.0       1.0         180   1620         59
## 216      770     432        48    16.0       2.0          95   1360         47
## 217      900     510        57    19.0       2.0         140   1050         51
## 218      990     580        65    24.0       2.0         160   1480         53
## 219      660     360        40    12.0       1.5          90    980         49
## 220      760     430        47    16.0       1.0         100   1410         53
## 221      340     170        19     5.0       0.0          40    510         28
## 222      380     210        23     8.0       1.0          55    730         29
## 223      590     360        40    12.0       0.0         150   1540         18
## 224      720     450        50    13.0       0.0         120   1960         32
## 225      550     330        37    10.0       0.0         115   1640         17
## 226      690     430        48    12.0       1.0         100   1750         31
## 227      530     290        32     5.0       0.0          95   1640         26
## 228      670     380        43     7.0       0.0          80   1760         40
## 229      560     270        30     7.0       0.0          90    980         40
## 230      700     370        41     9.0       0.0          80   1090         54
## 231      320     120        14     6.0       0.0         115    650         16
## 232      450     220        24     7.0       0.0          85   1070         30
## 233      220     180        20     4.0       0.0          10    540          7
## 234      230     190        21     5.0       0.0          30    520          7
## 235      830     468        52    14.0       0.5         110   2100         57
## 236      440     243        27     4.5       0.0          15    630         44
## 237      530     250        27     4.5       0.0          30   1360         54
## 238      410     150        16     3.0       0.0           5   1030         44
## 239      480     220        25     2.5       0.0           5   1160         42
## 240      730     351        39     9.0       0.0          90   1930         63
## 241      290     150        17     3.0       1.5          40    780         18
## 242      190     100        11     2.0       0.0          25    310         10
## 243      290     150        17     3.0       0.0          40    460         15
## 244      950     500        55    11.0       0.0         130   1530         50
## 245      470     260        29     5.0       0.0          50    890         34
## 246      570     225        25     8.0       0.0          70   1340         57
## 247      580     252        28     8.0       0.5          70   2310         56
## 248      430     250        28     4.5       0.0          30    760         34
## 249      670     370        41     7.0       0.5          60   1070         54
## 250      470     170        19     3.5       0.0          85    850         39
## 251      330     170        19     8.0       1.0          40    980         28
## 252      310     140        16     6.0       1.0          30    960         32
## 253      300     160        18     3.0       0.0          40    950         19
## 254      630     350        39     7.0       1.0          65   1390         46
## 255      340     189        21     3.5       0.0          45   1200         21
## 256      410     150        17     3.0       0.0          20    870         53
## 257      840     459        51    12.0       1.0          95   1760         62
## 258      210     135        15     3.0       0.0          20    570         11
## 259      530     333        37     7.0       0.0          55   1420         28
## 260      410     220        25     4.5       0.0          35    850         35
## 261      700     378        42     7.0       0.0          65   1140         57
## 262      760     405        45    11.0       0.0          95   1720         58
## 263     1000     660        74    26.0       2.0         170   1610         40
## 264      800     460        51    20.0       2.0         135   1280         44
## 265      630     330        37    13.0       1.0          95   1250         44
## 266      540     270        30    11.0       1.0          70   1020         44
## 267      570     310        35    11.0       1.0          75    820         39
## 268      400     160        18     9.0       1.0          65    930         34
## 269      630     310        34    18.0       2.0         125   1240         34
## 270     1030     480        53     9.0       1.0          80   2780        105
## 271     1260     590        66    11.0       1.0         120   3500        121
## 272      420     240        26    11.0       1.0          60   1140         26
## 273      390     220        24    11.0       1.0          50   1000         26
## 274      380     220        24    11.0       1.0          55    900         23
## 275      330     180        20     8.0       1.0          40   1050         24
## 276      290     160        17     7.0       1.0          35    900         22
## 277      350     180        20     8.0       1.0          35   1000         30
## 278      310      80         9     3.0       0.0          50    830         41
## 279      250      80         9     1.0       0.0           0    500         36
## 280      550     410        45    25.0       0.0         150    900          0
## 281     1050     670        75    43.0       1.0         180   2210         52
## 282      760     440        49    21.0       2.0         100   1570         48
## 283      260     140        15     4.0       0.0          20    450         26
## 284      470     200        22     3.0       0.0          20   1210         53
## 285      400     160        18     9.0       1.0          65    930         35
## 286      640     310        34    18.0       2.0         125   1240         35
## 287      540     240        26    13.0       1.0         100    750         34
## 288      350     130        14     7.0       1.0          50    680         34
## 289      780     430        48    22.0       2.0         150   1390         34
## 290      580     310        34     7.0       0.0          45    910         48
## 291      910     430        48    13.0       0.5          45   2210         95
## 292      350     180        20     3.0       0.0          60    960         22
## 293      500     180        20     8.0       0.0          65   1190         45
## 294      640     220        25     8.0       0.0          60   1530         68
## 295      520     280        31    10.0       0.0         100   1470         25
## 296      280     120        13     2.0       0.0          40    670         24
## 297      600     270        30     5.0       0.0          55   1250         59
## 298      350     190        21     5.0       0.0          35    820         30
## 299      380     170        19     9.0       0.0         100   1540         11
## 300      150      20         2     0.5       0.0          40    730         10
## 301      360     140        15     3.0       0.0          50   1040         32
## 302      280     130        15     4.0       0.0          30    800         22
## 303       20       0         0     0.0       0.0           0     15          5
## 304      550     240        26     8.0       0.0          60   1420         45
## 305      320      80         9     4.0       0.0          20    680         43
## 306      640     160        18     8.0       0.0          40   1360         86
## 307      430     160        18     6.0       0.0          50    590         47
## 308      860     320        36    12.0       0.0         100   1180         94
## 309      580     310        31    11.0       0.0          85   1470         47
## 310     1160     620        62    22.0       0.0         170   2940         94
## 311      500     150        17     9.0       1.0          85   1310         51
## 312     1000     300        34    18.0       2.0         170   2620        102
## 313      180      20         3     0.5       0.0          10    450         30
## 314      290      40         5     1.0       0.0          20    830         46
## 315      580      80        10     2.0       0.0          40   1660         92
## 316      330      45         5     1.0       0.0          45    890         45
## 317      660      90        10     2.0       0.0          90   1780         90
## 318      570     230        26     7.0       0.0          70   1600         46
## 319     1140     460        52    14.0       0.0         140   3200         92
## 320      570     250        28    10.0       1.0          95   1080         47
## 321     1140     500        56    20.0       2.0         190   2160         94
## 322      460     140        16     6.0       0.0          80   1140         49
## 323      920     280        32    12.0       0.0         160   2280         98
## 324      370     120        13     4.0       0.0          50   1140         46
## 325      740     240        26     8.0       0.0         100   2280         92
## 326      470     130        15     4.5       0.0          85   1770         45
## 327      940     260        30     9.0       0.0         170   3540         90
## 328      410     150        16     6.0       0.0          45   1300         46
## 329      820     300        32    12.0       0.0          90   2600         92
## 330      550     260        29    10.0       0.0          75   1470         47
## 331     1100     520        58    20.0       0.0         150   2940         94
## 332      480     160        18     7.0       1.0          30    950         59
## 333      960     320        36    14.0       2.0          60   1900        118
## 334      320      40         5     2.0       0.0          25    640         47
## 335      640      80        10     4.0       0.0          50   1280         44
## 336      200      25         3     1.0       0.0          25    390         30
## 337      320      40         5     2.0       0.0          40    700         45
## 338      640      80        10     4.0       0.0          80   1400         90
## 339      350      50         6     1.5       0.0          50    540         44
## 340      700     100        12     3.0       0.0         100   1080         88
## 341      480     220        24     9.0       1.0          50   1520         46
## 342      960     440        48    18.0       2.0         100   3040         92
## 343      380      90        10     5.0       0.0          50   1060         48
## 344      760     180        20    10.0       0.0         100   2120         96
## 345      310      40         5     2.0       0.0          40    880         46
## 346      620      80        10     4.0       0.0          80   1760         92
## 347      370     100        11     5.0       0.0          45   1210         47
## 348      740     200        22    10.0       0.0          90   1420         94
## 349      420     170        19     3.0       0.0          20    690         51
## 350      840     340        38     6.0       0.0          40   1380        102
## 351      380      40         5     1.0       0.0          50    900         59
## 352      760      80        10     2.0       0.0         100   1800        118
## 353      470     210        24     4.0       0.0          30    620         44
## 354      940     420        48     8.0       0.0          60   1240         88
## 355      390     110        13     3.5       0.0          30    860         49
## 356      780     220        26     7.0       0.0          60   1720         98
## 357      180      20         2     0.5       0.0          10    380         30
## 358      280      30         4     1.0       0.0          20    810         46
## 359      560      60         8     2.0       0.0          40   1620         92
## 360      280      35         4     1.0       0.0          20    820         46
## 361      560      70         8     2.0       0.0          40   1640         92
## 362      490     210        24     9.0       1.0          50   1480         47
## 363      980     420        48    18.0       2.0         100   2960         94
## 364      150      15         2     0.0       0.0           0    190         29
## 365      230      20         3     1.0       0.0           0    310         44
## 366      460      40         6     2.0       0.0           0    620         88
## 367      390      70         7     1.0       0.0          10    800         56
## 368      780     140        14     2.0       0.0          20   1600        112
## 369      300      80         9     3.0       0.0          60   1120         26
## 370      150      70         8     4.0       0.0          20    420         10
## 371      400     300        29    11.0       0.0          85   1250         12
## 372      330     140        16     8.0       1.0          85   1080         17
## 373      110      25         3     1.0       0.0          20    590         11
## 374      360     230        26     4.0       0.0          60   1100         13
## 375      280     110        12     4.5       0.0          65   1320         11
## 376      150      30         4     0.0       0.0          45    680          8
## 377      510     340        38    12.0       1.0         100   1040         14
## 378      180      95        11     4.0       0.0          45    820         12
## 379      220      35         5     1.5       0.0         100    490         10
## 380      230     135        15     6.0       0.0          45   1060         12
## 381      230     140        15     5.0       0.0          45   1060         13
## 382      310     150        17     7.0       1.0          30    720         25
## 383      140      25         3     0.5       0.0          50    280         10
## 384      140      30         4     1.0       0.0          40    450         10
## 385      310     205        23     9.0       1.0          50   1280         11
## 386      210      75         8     4.0       0.0          50    830         14
## 387      140      30         4     1.0       0.0          40    640         11
## 388      200      85        10     5.0       0.0          45    910         13
## 389      200      25         3     1.0       0.0          50    660         24
## 390      310     215        24     4.0       0.0          40    370         10
## 391      110      20         3     1.0       0.0          25    580         11
## 392      110      20         2     1.0       0.0          20    570         11
## 393       50      10         1     0.0       0.0           0     65          9
## 394      760     330        37    12.0       1.0         100   2250         65
## 395      730     310        34    10.0       0.5         135   1900         53
## 396      810     380        42    13.0       0.5          75   2970         62
## 397      740     230        25    11.0       0.0          50   1270        100
## 398      680     200        22     9.0       0.0          40   1070         96
## 399      790     290        32    13.0       0.0          60   1350         96
## 400      820     310        34    14.0       0.0          70   1420         97
## 401      540     230        26     7.0       1.0          45   1360         59
## 402      460     170        18     7.0       1.0          45   1320         53
## 403      510     170        19     7.0       0.0          20   1090         68
## 404      370     100        11     4.0       0.0           5    960         56
## 405      550     200        22     8.0       0.0          35   1270         68
## 406      440     160        18     5.0       0.0          20   1030         55
## 407      410     110        12     4.0       0.0          10   1100         62
## 408      420     140        16     7.0       0.0          35   1090         53
## 409      390     110        12     5.0       0.0          40   1050         52
## 410      390     120        13     5.0       0.0          30   1090         52
## 411      760     240        27     6.0       0.0          60   1960         96
## 412      780     250        28     7.0       0.0          50   1900         98
## 413      740     230        26     5.0       0.0          10   1750        107
## 414      420     160        17     3.5       0.0           0    930         55
## 415      380     150        17     8.0       1.0          35    930         41
## 416      610     210        24     9.0       0.0          55   1510         74
## 417      610     220        24     9.0       0.0          50   1520         75
## 418      630     240        26    10.0       0.5          45   1530         76
## 419      550     260        29     9.0       0.5          50   1130         52
## 420      620     270        30    10.0       0.0          60   1440         64
## 421      630     280        31    11.0       0.5          65   1410         64
## 422      650     300        34    12.0       0.5          60   1450         65
## 423      400     160        18     4.5       0.0          30    960         45
## 424      710     320        35    13.0       1.0          75   2260         70
## 425      650     250        28    10.0       0.0          70   2230         67
## 426      670     260        29    11.0       0.5          80   2080         68
## 427      540     180        20     8.0       0.0          55   1740         66
## 428      550     190        21     9.0       0.0          50   1750         66
## 429      570     210        23    10.0       0.5          45   1760         68
## 430      410     140        16     6.0       0.0          30   1030         50
## 431      880     380        42    14.0       1.0          75   2020         94
## 432      830     320        35    11.0       0.0          85   1940         91
## 433      820     320        36    12.0       1.0          70   2020         91
## 434      170      50         6     3.0       0.0          30    460         18
## 435      320     120        14     5.0       0.0          25    770         36
## 436      160      90        10     3.5       0.0          25    350         13
## 437      200     100        12     4.5       0.0          35    370         15
## 438      170      90        10     4.0       0.0          25    290         12
## 439      200     110        12     5.0       0.0          35    320         15
## 440      320     120        14     5.0       0.0          25    640         37
## 441      350     140        16     6.0       0.0          35    670         40
## 442      340     160        18     7.0       0.0          35    640         32
## 443      350     180        20     8.0       0.5          40    630         30
## 444      380     170        19     6.0       0.0          35    650         39
## 445      320     120        13     5.0       0.0          25    770         36
## 446      170      90        10     3.5       0.0          25    370         12
## 447      200     110        12     5.0       0.0          30    390         15
## 448      250     130        14     4.0       0.0          30    550         19
## 449      320     120        13     5.0       0.0          25    760         36
## 450      170      80         9     4.0       0.0          25    340         13
## 451      200     100        11     5.0       0.0          35    370         15
## 452      230     100        11     5.0       0.0          35    530         22
## 453      200      80         9     4.0       0.0          25    510         19
## 454      250     120        13     3.0       0.0          10    510         28
## 455      340     160        18     4.0       0.0          40    530         29
## 456      340     170        18     4.0       0.0          30    570         29
## 457      370     190        21     5.0       0.0          30    570         31
## 458      600     310        35     8.0       0.5          50   1010         50
## 459      420     250        28     6.0       0.0          65   1070         23
## 460      440     270        30     7.0       0.0          70   1090         22
## 461      600     310        35     8.0       0.5          50   1240         52
## 462      350      80         9     3.0       0.0           0    950         57
## 463      340      80         8     3.0       0.0          25   1020         50
## 464      340      80         9     3.0       0.0          15   1060         50
## 465      150      35         4     1.0       0.0          25    460         18
## 466      140      70         8     2.0       0.0          20    290         13
## 467      150      35         4     2.0       0.0          15    500         19
## 468      170      60         7     3.0       0.0          20    500         20
## 469      490     260        29    10.0       1.0          55    810         39
## 470      490     250        28    10.0       1.0          55    890         40
## 471      490     250        28    10.0       1.0          55    890         40
## 472      490     250        28    10.0       1.0          55    880         40
## 473      570     290        32    12.0       1.0          70   1110         44
## 474      300     120        14     5.0       0.0          30    550         31
## 475      270      90        10     4.0       0.0          40    510         29
## 476      270      90        11     4.0       0.0          30    550         29
## 477      710     360        41     6.0       0.0          30   1420         73
## 478      760     360        39     6.0       0.0          30   1100         82
## 479      430     210        23     5.0       0.0          30    690         44
## 480      320     140        15     1.5       0.0           0    600         41
## 481      260     140        16     4.5       0.0          30    550         19
## 482      410     170        19     6.0       0.0          25    960         46
## 483      210     110        12     4.0       0.0          25    560         17
## 484      420     170        19     4.5       0.0          20    870         49
## 485      430     210        23     5.0       0.0          20    900         43
## 486      560     200        22     4.0       0.0          60   1520         64
## 487      580     210        23     4.0       0.0          50   1460         66
## 488      540     190        21     3.0       0.0          10   1310         75
## 489      480     240        27    11.0       1.0          50   1000         40
## 490      190      80         9     5.0       0.0          20    450         18
## 491      520     250        28    12.0       1.0          75   1210         41
## 492      620     340        37     8.0       0.0          50   1290         53
## 493      380     150        17     8.0       1.0          35    930         41
## 494      290     170        18     3.0       0.0          25    640         22
## 495      650     340        37    13.0       0.5          75   1480         51
## 496      540     190        21     6.0       0.0          30   1110         71
## 497      270     100        11     4.0       0.0          15    650         32
## 498      580     260        29     9.0       1.0          60   1270         59
## 499      470     200        22     6.0       0.0          25   1120         55
## 500      540     270        31     8.0       1.0          40    860         47
## 501      270     130        14     7.0       1.0          40    740         21
## 502      440     210        23    10.0       0.5          60    840         36
## 503      440     200        23    10.0       0.5          60    840         37
## 504      460     240        26    11.0       1.0          50    890         38
## 505      180      70         8     2.5       0.0          25    540         15
## 506      400     180        20     4.0       0.0          25    900         42
## 507      200      90        10     2.5       0.0          10    440         22
## 508      390     170        18     8.0       0.5          40   1050         39
## 509      520     250        28    12.0       1.0          65   1250         41
## 510      700     270        30     9.0       0.5          45   1550         85
## 511      780     340        38    10.0       0.5          50   1850         87
## 512      580     260        29     9.0       1.0          60   1270         59
## 513      780     380        42    10.0       1.0          60   1340         74
## 514      720     320        35     7.0       0.0          70   1260         70
## 515      720     320        36     8.0       1.0          55   1340         70
##     fiber sugar protein vit_a vit_c calcium salad
## 1       3    11      37     4    20      20 Other
## 2       2    18      46     6    20      20 Other
## 3       3    18      70    10    20      50 Other
## 4       2    18      55     6    25      20 Other
## 5       4    18      46     6    20      20 Other
## 6       3     9      25    10     2      15 Other
## 7       2     7      15    10     2      10 Other
## 8       3     6      25     0     4       2 Other
## 9       2     7      25    20     4      15 Other
## 10      3    10      51    20     6      20 Other
## 11      2     5      15     2     0      15 Other
## 12      3    11      32    10    10      35 Other
## 13      3    11      42    10    20      35 Other
## 14      5    11      33    10    15      35 Other
## 15      2     6      13     2     2       4 Other
## 16      2     3      24     4     6      15 Other
## 17      3    10      37     6    15      15 Other
## 18      3    14      48     4    30      30 Other
## 19      5    14      39     4    20     290 Other
## 20      2     5      15     2     2       4 Other
## 21      2     7      23    10     2      10 Other
## 22      2    12      25     2     2       6 Other
## 23      4     7      29     8    15      15 Other
## 24      4    12      40     8    25      30 Other
## 25      6    12      31     8    15      30 Other
## 26      4    11      28     4    10      20 Other
## 27      3    13      25     6    10      20 Other
## 28      3    10      31    20     6      15 Other
## 29      4    13      32    20    15      30 Other
## 30      4    14      41    20    25      30 Other
## 31      5    13      32    20    20      30 Other
## 32      3    14      38     6    15      15 Other
## 33      4    18      48     4    30      25 Other
## 34      5    18      39     4    20      30 Other
## 35      0     0      28     0     0       2 Other
## 36      0     1      38     0     0       2 Other
## 37      1     1      58     0     0       2 Other
## 38      1     4      94     0     0       4 Other
## 39      1     2     115     0     2       6 Other
## 40      2     3     186     0     2       8 Other
## 41      1     0      10     0     2       0 Other
## 42      1     0      15     0     2       0 Other
## 43      2     0      24     0     4       2 Other
## 44      4     0      49     0     8       4 Other
## 45      7     1      98     0    15       6 Other
## 46      2    35      39     4    15       4 Other
## 47      3    52      58     4    25       8 Other
## 48      5    87      97     8    40      10 Other
## 49      5     7       7   180    45      10 Other
## 50      5    10      31   180    70      10 Other
## 51      4     4      33   180    60      15 Other
## 52      3     3      14   180    50      15 Other
## 53      3     4      42   180    60      15 Other
## 54      4     4      33   180    60      15 Other
## 55      6     9       8   180    40      20 Other
## 56      6     9      37   180    50      20 Other
## 57      8     9      28   180    40      20 Other
## 58      3     7      37    30    40      25 Other
## 59      3     7      29    25    40      10 Other
## 60      1     4      16    NA     0       2 Other
## 61      0     1      11     0     0       2 Other
## 62      1     1      22     0     2       4 Other
## 63      1     3      28     2     2       6 Other
## 64      1     4      37     2     4       8 Other
## 65      3     6      31    30    10      20 Other
## 66      1     0      14     0     2       2 Other
## 67      1     0      21     0     4       2 Other
## 68      1     1      28     0     2       4 Other
## 69      2     1      41     0     8       4 Other
## 70      4     1     103    NA    20      10 Other
## 71      5    12      28    35     8      15 Other
## 72      2     5      28     2     4      15 Other
## 73      0     0      13     0     6       0 Other
## 74      0     0      19     0     8       0 Other
## 75      0     0      25     0    10       2 Other
## 76      0     1      38     0    20       2 Other
## 77      5     9      33    NA    25      25 Other
## 78      4    10      34    NA    50      25 Other
## 79      2    10      33    45    40      20 Other
## 80      1     5      29     4     2      15 Other
## 81      2     6      34    30    10      30 Other
## 82     15     3      37    60    35      35 Other
## 83     NA     8      39    NA    NA      NA Other
## 84     NA     7      48    NA    NA      NA Other
## 85      2     7      35    10    25      30 Other
## 86      2     6      31     4     2      20 Other
## 87      1     6      15     2     4       6 Other
## 88      1     4      20     7     1      15 Other
## 89      1     4      15     2     4       6 Other
## 90      1     4      19     6     4      15 Other
## 91      1     7      31    15     4      25 Other
## 92      2     7      39    10     8      30 Other
## 93      2     7      31     6     8      20 Other
## 94      2    10      32     8    10      20 Other
## 95      2     7      31     6     8      20 Other
## 96      2     7      35    10     8      30 Other
## 97      2    10      35    15    10      30 Other
## 98      2     7      35    10     8      30 Other
## 99      2     7      67    15     6      40 Other
## 100     2     8      63    15     8      40 Other
## 101     2    11      63    20    10      40 Other
## 102     2     8      63    15     8      40 Other
## 103     2     7      63    15     2      40 Other
## 104     5    11      15     6     8      25 Other
## 105     5     8      15     6     8      27 Other
## 106     5     8      15     6     8      25 Other
## 107     3     8      40    11    20      16 Other
## 108     4     7      31    11     7      16 Other
## 109     2     6      28     6     8      10 Other
## 110     4     6      23     6     8      10 Other
## 111     1     4      19     0     0       4 Other
## 112     0     0      22    NA    NA      NA Other
## 113     0     0      37    NA    NA      NA Other
## 114     4    12      33    10     8      15 Other
## 115     5    12      23    NA    NA      NA Other
## 116     4    10      23    NA    NA      NA Other
## 117     3     1      18     0     0       2 Other
## 118     5     2      27     0     0       4 Other
## 119     2     0      21    10     0       2 Other
## 120     3     0      36    17     0       3 Other
## 121     7     9      30     1     6      13 Other
## 122     8     9      37     1     7      13 Other
## 123     8     9      44     2     8      14 Other
## 124     2     0      22     1     2       1 Other
## 125     2     1      29     1     2       1 Other
## 126     3     1      36     1     3       2 Other
## 127     3    11      32     4     2      15 Other
## 128     4    12      39    15     8      30 Other
## 129     1    15      12     2     4       8 Other
## 130     1    17      14     4     6      10 Other
## 131     2     4      17    10     2      20 Other
## 132     3     4      13     2    10       8 Other
## 133     1     3      11     0     2       8 Other
## 134     2     7      15     1     3       8 Other
## 135     2     4       6     0     0       4 Other
## 136     3     9      30    15     4      30 Other
## 137     1     2      11     0     0       4 Other
## 138     2     5      18     2     0       8 Other
## 139     3    23      18     4    10      10 Other
## 140     2     9      23     2     2      15 Other
## 141     2     9      39     2     2      15 Other
## 142     2    15      38    NA    NA      NA Other
## 143     3    16      38    NA    NA      NA Other
## 144     3    16      38    NA    NA      NA Other
## 145     2     6      29    NA    NA      NA Other
## 146     2     9      39    NA    NA      NA Other
## 147     1     7      41    NA    NA      NA Other
## 148     2     6      29    NA    NA      NA Other
## 149     2     3      35     2     8      15 Other
## 150     2     5      23     0     0       6 Other
## 151     2     5      38     0     0       6 Other
## 152     3     4      42    NA    NA      NA Other
## 153     2     9      30    15    10      15 Other
## 154     4     6      23    NA    NA      NA Other
## 155     2     9      49    NA    NA      NA Other
## 156     2     3      55    NA    NA      NA Other
## 157     2     5      48    NA    NA      NA Other
## 158     2     6      18     2     0      15 Other
## 159     3     7      32    NA    NA      NA Other
## 160     4     9      22    NA    NA      NA Other
## 161     6    20      33    10     8      25 Other
## 162     1     0      16     0     0       2 Other
## 163     2     0      23     0     4       2 Other
## 164     3     0      39     0     8       2 Other
## 165     4     5      37     6    20      35 Other
## 166     3     5      24    10    15      10 Other
## 167     5    15      38    20    10      45 Other
## 168     4     6      30    20    10      35 Other
## 169     5    16      45    20    10      45 Other
## 170     4     6      37    20    10      30 Other
## 171     4    17      43    NA    NA      NA Other
## 172     4    14      26    NA    NA      NA Other
## 173     2     7      33     4     8      20 Other
## 174     3    11      23    10    10       8 Other
## 175     2     9      30    NA    NA      NA Other
## 176     5    19      62    NA    NA      NA Other
## 177     6    16      41    NA    NA      NA Other
## 178     3     5      25    10    15      10 Other
## 179     6    19      43    NA    NA      NA Other
## 180     2     2      12    NA    NA      NA Other
## 181     1     1      15    NA    NA      NA Other
## 182     1     1      14    NA    NA      NA Other
## 183     1     2      13    NA    NA      NA Other
## 184     1     1      14    NA    NA      NA Other
## 185     1     2      13    NA    NA      NA Other
## 186     1     1      14    NA    NA      NA Other
## 187     1     2      14    NA    NA      NA Other
## 188     1     2       5    35    10      10 Other
## 189     4     4      28    60    20      25 Other
## 190     2     4      10    NA    NA      NA Other
## 191     2     5      22    60    20      25 Other
## 192     5     7      22    NA    NA      NA Other
## 193     3     7     134    NA    NA      NA Other
## 194     2     8      56    NA    NA      NA Other
## 195     1     7      18    NA    NA      NA Other
## 196     1     7      12    NA    NA      NA Other
## 197     1    10      57    NA    NA      NA Other
## 198     0    16      32    NA    NA      NA Other
## 199    NA    13      57    NA    NA      NA Other
## 200     1     6      16    NA    NA      NA Other
## 201     1     8      31    NA    NA      NA Other
## 202     1     6      26    NA    NA      NA Other
## 203     1     6      22    NA    NA      NA Other
## 204     2    11      56    NA    NA      NA Other
## 205     2     9      26    NA    NA      NA Other
## 206    NA    15      NA    NA    NA      NA Other
## 207     1     6      13    NA    NA      NA Other
## 208     2    10      30    NA    NA      NA Other
## 209     2     7      55    NA    NA      NA Other
## 210    NA     8      49    NA    NA      NA Other
## 211     1     9       9    NA    NA      NA Other
## 212     3    14      60    NA    NA      NA Other
## 213     2    12      35    NA    NA      NA Other
## 214     2    12      55    NA    NA      NA Other
## 215    NA    13      50    NA    NA      NA Other
## 216     2     9      29    NA    NA      NA Other
## 217     3    11      47    NA    NA      NA Other
## 218     3    11      52    NA    NA      NA Other
## 219     2    11      28    NA    NA      NA Other
## 220     3    11      33    NA    NA      NA Other
## 221     2     6      14    NA    NA      NA Other
## 222     2     6      16    NA    NA      NA Other
## 223     3     6      42    NA    NA      NA Other
## 224     5     7      36    NA    NA      NA Other
## 225     3     5      36    NA    NA      NA Other
## 226     4     8      35    NA    NA      NA Other
## 227     3     6      35    NA    NA      NA Other
## 228     5     8      34    NA    NA      NA Other
## 229     4    34      29    NA    NA      NA Other
## 230     5    37      28    NA    NA      NA Other
## 231     2     4      36    NA    NA      NA Other
## 232     5     6      29    NA    NA      NA Other
## 233     2     3       6    NA    NA      NA Other
## 234     2     3       5    NA    NA      NA Other
## 235    NA     9      34    NA    NA      NA Other
## 236    NA    13       7    NA    NA      NA Other
## 237     2     7      17    NA    NA      NA Other
## 238     7     8      22    NA    NA      NA Other
## 239     2    10      22    NA    NA      NA Other
## 240    NA    16      32    NA    NA      NA Other
## 241     1     1      16    NA    NA      NA Other
## 242     1     0      10    NA    NA      NA Other
## 243     1     0      15    NA    NA      NA Other
## 244     5     0      51    NA    NA      NA Other
## 245     5     0      21    NA    NA      NA Other
## 246    NA     9      32    NA    NA      NA Other
## 247    NA     8      30    NA    NA      NA Other
## 248     2     4      12    NA    NA      NA Other
## 249     2     7      23    NA    NA      NA Other
## 250     2     6      37    NA    NA      NA Other
## 251     2     5      14    NA    NA      NA Other
## 252     2    10      11    NA    NA      NA Other
## 253     1     1      15    NA    NA      NA Other
## 254     3     4      24    NA    NA      NA Other
## 255     1     1      16    NA    NA      NA Other
## 256     2    14      12    NA    NA      NA Other
## 257     3     7      32    NA    NA      NA Other
## 258     2     0       8    NA    NA      NA Other
## 259    NA     0      20    NA    NA      NA Other
## 260     2     5      12    NA    NA      NA Other
## 261     3     8      25    NA    NA      NA Other
## 262     3     8      32    NA    NA      NA Other
## 263     2     9      46    25     8      30 Other
## 264     3    13      40    25     6      35 Other
## 265     2    13      30    20     6      25 Other
## 266     3    13      23    20     6      25 Other
## 267     2     8      24     2     0      25 Other
## 268     1     8      19    10     0      10 Other
## 269     1     9      34    15     0      20 Other
## 270     9     4      35     2     0      10 Other
## 271    12     4      49     2     0      10 Other
## 272     1     3      19    NA    NA      NA Other
## 273     1     3      16    NA    NA      NA Other
## 274     1     3      16    10     0      15 Other
## 275     1     5      13     8     0       6 Other
## 276     1     4      11     4     0       6 Other
## 277     1     6      13    NA    NA      NA Other
## 278     2     9      17    10     4       4 Other
## 279     2     1       7     0     2       2 Other
## 280     0     0      35    30     0     100 Other
## 281     0    30      43    NA    NA      NA Other
## 282     2     6      32    NA    NA      NA Other
## 283     1     7       6     0     4       0 Other
## 284     2     7      17    10     2       6 Other
## 285     1     9      20    20     6      10 Other
## 286     1     9      34    25     6      20 Other
## 287     1     9      29    15     6       4 Other
## 288     1     9      17    15     6       4 Other
## 289     1     7      41    20     6      20 Other
## 290     2     6      19    NA    NA      NA Other
## 291     5     2      23    NA    NA      NA Other
## 292    10     0      22    NA    NA      NA Other
## 293     3     3      33    NA    NA      NA Other
## 294     4     3      34    NA    NA      NA Other
## 295     9     6      37    NA    NA      NA Other
## 296     9     6      17    NA    NA      NA Other
## 297     7     8      24    10     6      15 Other
## 298     2     1      12    10     2      10 Other
## 299     3     6      42    NA    NA      NA Other
## 300     3     6      23    NA    NA      NA Other
## 301     1     5      25    10     8       6 Other
## 302     1     1      15    10     4      10 Other
## 303     2     3       1    50    30      15 Other
## 304     3     3      30    NA    NA      NA Other
## 305     5     6      15     8     8      30 Other
## 306    10    12      30    16    16      60 Other
## 307     5     8      19     8    20      30 Other
## 308    10    16      38    16    40      60 Other
## 309     5     7      29    10    45      40 Other
## 310    10    14      58    20    90      80 Other
## 311     6     8      38    15    20      50 Other
## 312    12    16      76    30    40     100 Other
## 313     3     5      10     6    15      20 Other
## 314     5     8      18     8    20      30 Other
## 315    10    16      36    16    40      60 Other
## 316     5     7      25     8    20      30 Other
## 317    10    14      50    16    40      60 Other
## 318     5     8      33    10    20      40 Other
## 319    10    16      66    20    40      80 Other
## 320     5     8      35    15    25      50 Other
## 321    10    16      70    30    50     100 Other
## 322     6     9      32    15    30      45 Other
## 323    12    18      64    30    60      90 Other
## 324     5     7      18    10    20      35 Other
## 325    10    14      36    20    40      70 Other
## 326     7    12      39    10    35      20 Other
## 327    14    24      78    20    70      40 Other
## 328     5     8      20     8    20      30 Other
## 329    10    16      40    16    40      60 Other
## 330     5     9      26    10    20      40 Other
## 331    10    18      52    20    40      80 Other
## 332     8    12      21    25    35      35 Other
## 333    16    24      42    50    70      70 Other
## 334     5     8      23     8    30      30 Other
## 335    10    16      46    16    60      60 Other
## 336     4     5      14     6    15      20 Other
## 337     5     7      24     8    20      30 Other
## 338    10    14      48    16    40      60 Other
## 339     5     7      29     8    20      30 Other
## 340    10    14      58    16    40      60 Other
## 341     5     8      20     8    20      30 Other
## 342    10    16      40    16    40      60 Other
## 343     5     8      26    10    20      40 Other
## 344    10    16      52    20    40      80 Other
## 345     5     7      23     8    20      30 Other
## 346    10    14      46    16    40      60 Other
## 347     5     8      23    10    20      40 Other
## 348    10    16      46    20    40      80 Other
## 349     5     8      13    10    20      35 Other
## 350    10    16      26    20    40      70 Other
## 351     5    18      26     8    30      35 Other
## 352    10    36      52    16    60      70 Other
## 353     5     6      20     8    20      30 Other
## 354    10    12      40    16    40      60 Other
## 355     8     7      22    10   200      30 Other
## 356    16    14      44    20   400      60 Other
## 357     3     5      10     6    15      20 Other
## 358     5     7      18     8    20      30 Other
## 359    10    14      36    16    40      60 Other
## 360     5     8      18     8    20      30 Other
## 361    10    16      36    16    40      60 Other
## 362     5     8      24    10    20      45 Other
## 363    10    16      48    20    40      90 Other
## 364     3     4       6     6    15      20 Other
## 365     5     6       8     8    20      30 Other
## 366    10    12      16    16    40      60 Other
## 367     8     8      23    15    20      35 Other
## 368    16    16      46    30    20      70 Other
## 369     3    22      25    40    40      15 Other
## 370     4     5      10    50    50       6 Other
## 371     4     4      23    25    70      10 Other
## 372     5     6      32    60    50      25 Other
## 373     4     6      12    25    45       4 Other
## 374     4     6      20    50    60       8 Other
## 375     4     5      28    50    50      15 Other
## 376     3     3      19    40    40       6 Other
## 377     4     7      30    60    60      30 Other
## 378     4     5      12    50    50      10 Other
## 379     4     4      36    50    60       8 Other
## 380     4     6      14    50    50       6 Other
## 381     4     8      14    40    60       4 Other
## 382     6    10      16    60    70      10 Other
## 383     4     4      19    50    60       8 Other
## 384     4     5      18    25    45       4 Other
## 385     4     6      15    50    50       8 Other
## 386     4     6      20    50    50      15 Other
## 387     4     5      17    25    45       6 Other
## 388     4     6      18    50    50      15 Other
## 389     4    16      20    25    50       6 Other
## 390     4     4      15    50    50       6 Other
## 391     4     5      12    25    45       6 Other
## 392     4     5      12    25    45       6 Other
## 393     4     4       3    25    45       4 Other
## 394     4     7      43    15    45      30 Other
## 395     3     4      55    15     8      45 Other
## 396     3     6      43    10    30      30 Other
## 397     5     9      36    35    30      60 Other
## 398     4     7      32    25     4      45 Other
## 399     4     8      38    30     4      60 Other
## 400     4     8      39    30     4      60 Other
## 401     7     4      19    NA    NA      NA Other
## 402     9     3      21    NA    NA      NA Other
## 403    11     4      16    NA    NA      NA Other
## 404     9     3      13    NA    NA      NA Other
## 405     8     5      19    NA    NA      NA Other
## 406     4     3      13    NA    NA      NA Other
## 407     8     3      14    NA    NA      NA Other
## 408     8     5      16    NA    NA      NA Other
## 409     7     5      19    NA    NA      NA Other
## 410     7     5      17    NA    NA      NA Other
## 411    12     7      32    NA    NA      NA Other
## 412    13     7      33    NA    NA      NA Other
## 413    17     8      20    NA    NA      NA Other
## 414     6     4      11    NA    NA      NA Other
## 415     5     2      16    NA    NA      NA Other
## 416     5     5      25    10     4      35 Other
## 417     5     5      25    10     4      40 Other
## 418     7     5      22    15     4      35 Other
## 419     7     4      20    15     6      20 Other
## 420     4     4      24    NA    NA      NA Other
## 421     3     4      25    NA    NA      NA Other
## 422     6     5      22    NA    NA      NA Other
## 423     3     3      16    NA    NA      NA Other
## 424    10     4      28    NA    NA      NA Other
## 425     8     4      34    NA    NA      NA Other
## 426     7     4      35    NA    NA      NA Other
## 427     5     5      24    15     8      35 Other
## 428     5     5      24    10     6      35 Other
## 429     7     5      22    15     6      35 Other
## 430     4     3      15     6     2      20 Other
## 431    12     6      31    NA    NA      NA Other
## 432    10     6      37    NA    NA      NA Other
## 433    10     7      33    NA    NA      NA Other
## 434     1     1      12    NA    NA      NA Other
## 435     6     2      13    NA    NA      NA Other
## 436     2     1       8    NA    NA      NA Other
## 437     3     3       9    NA    NA      NA Other
## 438     3     1       8    NA    NA      NA Other
## 439     3     2       9    NA    NA      NA Other
## 440     7     2      13    NA    NA      NA Other
## 441     7     3      14    NA    NA      NA Other
## 442     4     6      12    10     2      15 Other
## 443     4     3      13    15     2      20 Other
## 444     5     2      13     8     2      20 Other
## 445     7     2      14    NA    NA      NA Other
## 446     3     1       8    NA    NA      NA Other
## 447     3     2       9    NA    NA      NA Other
## 448     2     2      11    NA    NA      NA Other
## 449     7     2      14    NA    NA      NA Other
## 450     2     1       8    NA    NA      NA Other
## 451     3     2       9    NA    NA      NA Other
## 452     3     3      10    NA    NA      NA Other
## 453     3     1      10    NA    NA      NA Other
## 454     3     1       6    NA    NA      NA Other
## 455     3     4      16    NA    NA      NA Other
## 456     3     4      14    NA    NA      NA Other
## 457     4     4      13    NA    NA      NA Other
## 458     6     5      21    15     4      15 Other
## 459     4     2      19     6     4       6 Other
## 460     3     1      20     6     4       6 Other
## 461     7     5      21    15     8      15 Other
## 462     9     3      11    NA    NA      NA Other
## 463     7     4      17    NA    NA      NA Other
## 464     7     4      15    NA    NA      NA Other
## 465     2     2      11    NA    NA      NA Other
## 466     3     1       6    NA    NA      NA Other
## 467     2     2       9    NA    NA      NA Other
## 468     3     2       8    NA    NA      NA Other
## 469     5     6      20    NA    NA      NA Other
## 470     5     5      20    NA    NA      NA Other
## 471     5     4      20    NA    NA      NA Other
## 472     5     5      20    NA    NA      NA Other
## 473     7     5      25    15     2      30 Other
## 474     4     6      13    NA    NA      NA Other
## 475     2     6      16    NA    NA      NA Other
## 476     2     6      14    NA    NA      NA Other
## 477    10     4      13    10     4       8 Other
## 478    13     5      18    NA    NA      NA Other
## 479     7     3      12    NA    NA      NA Other
## 480     6     2       7    NA    NA      NA Other
## 481     3     1      10     6     0      10 Other
## 482     4     3      14    NA    NA      NA Other
## 483     3     1       9    NA    NA      NA Other
## 484     5     3      12    NA    NA      NA Other
## 485     3     4      12    NA    NA      NA Other
## 486     9     4      26    NA    NA      NA Other
## 487    10     4      27    NA    NA      NA Other
## 488    14     4      14    NA    NA      NA Other
## 489     4     3      19    NA    NA      NA Other
## 490     2     1       9    NA    NA      NA Other
## 491     4     3      27    NA    NA      NA Other
## 492     4     4      17     8     6      15 Other
## 493     5     2      16    NA    NA      NA Other
## 494     1     1       9    NA    NA      NA Other
## 495     5     3      26    10     2      45 Other
## 496     7     7      16    NA    NA      NA Other
## 497     8     2      12    NA    NA      NA Other
## 498     8     7      23    NA    NA      NA Other
## 499     4     5      13    NA    NA      NA Other
## 500     7     2      20    NA    NA      NA Other
## 501     3     2      14    NA    NA      NA Other
## 502     3     3      22    15     6      35 Other
## 503     3     3      22    15     8      35 Other
## 504     4     3      19    15     6      35 Other
## 505     2     1      12    NA    NA      NA Other
## 506     3     3      15    NA    NA      NA Other
## 507     4     1       7    NA    NA      NA Other
## 508     4     3      18     8     2      30 Other
## 509     4     3      25    NA    NA      NA Other
## 510     9     7      23    15     6      25 Other
## 511     9     8      23    20    10      25 Other
## 512     8     7      23    NA    NA      NA Other
## 513    11     7      26    NA    NA      NA Other
## 514     8     8      32    NA    NA      NA Other
## 515     8     8      28    NA    NA      NA Other
```

Lets first check the resuturant and check the distrubution


```r
resturant <- table(data$restaurant)
pie(resturant)
```

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-2-1.png" width="672" />


lets check the distrubution of the total cals of each food item.


```r
hist(data$calories)
```

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-3-1.png" width="672" />

As we can see most of food item has calories around 500.


```r
cholesterol_fit <- linear_reg() %>%
  set_engine("lm") %>%
  fit(cholesterol ~ cal_fat + total_fat + trans_fat, data = data)
tidy(cholesterol_fit)
```

```
## # A tibble: 4 × 5
##   term        estimate std.error statistic  p.value
##   <chr>          <dbl>     <dbl>     <dbl>    <dbl>
## 1 (Intercept)   6.11      2.84      2.15   3.20e- 2
## 2 cal_fat       0.230     0.0967    2.38   1.76e- 2
## 3 total_fat     0.0655    0.874     0.0750 9.40e- 1
## 4 trans_fat    20.7       2.44      8.50   2.10e-16
```





