# Serializer changes

## 1.4.53

### v1/v2

#### `OrderLineGoogleAdsPremiumSerializer`

* Add `ticket_id` field, not required.

## 1.4.52

### v1/v2

#### `OrderLineDisplayNativeSerializer`

* Introduced new serializer - `OrderLineDisplayNativeSerializer`

## 1.4.51

### v1/v2

#### `OrderLineInAppSerializer`

* Set `poi_targeting_file` as not required.

## 1.4.50

### v1/v2

#### `OrderLineInAppSerializer`

* Add `poi_targeting_file` field.

## 1.4.49

### v1/v2

#### `OrderLineSerializer`

* Add `is_pre_briefing_necessary` field, default value is False.

## 1.4.48

### v1/v2

#### `OrderLineDisplayPremiumSerializer`

* Add validation for `impressions_per_month` and `impressions_one_time`, depending on `booking_type` (continuous or fixed).

## 1.4.47

### v1/v2

#### `OrderLineDisplayPremiumSerializer`

* Changed field `impressions_per_day` to `impressions_one_time`.

## 1.4.45

### v1/v2

#### `OrderLineDisplayPremiumSerializer`

* Changed field `age_targeting` choices: `DISPLAY_AGE_CHOICES`, removed legacy `[DISPLAY_AGE_14_19, DISPLAY_AGE_20_29]` and added `DISPLAY_AGE_14_29`

## 1.4.44
### v1/v2

* removed `detail_google_ads_basic` from `OrderLineSerializer`
* removed `OrderLineGoogleAdsBasicSerializer`

## 1.4.43
### v2

* removed `detail_display_basic` from `OrderLineSerializer`
* removed `OrderLineDisplayBasicSerializer`


## 1.4.42

### v1

#### `OrderLineGoogleAdsPremiumSerializer`

* Add field `branch_codes`, optional.


## 1.4.39

### v1/v2

#### `OrderLineDisplayPremiumSerializer`

* Add new field `short_name`, optional.

## 1.4.37

### v1/v2

#### `OrderLineEmailSerializer`

* Add necessary and additional fields for domain creation on email orderline: `desired_domain`, `domain_type` and `domain_info`.


## 1.4.36

### v1/v2

#### `OrderLineGoogleAdsPremiumSerializer`

* Add new fields for generic campaign information: `is_generic_campaign` and `generic_topics`, optionals.

## 1.4.34

### v1/v2

#### `OrderLineSeoSerializer`

* Make `ticket_id` optional.

## 1.4.33

### v1/v2

#### `ContactSerializer`

* Add new field `opt_in_marketing`, optional.

## 1.4.32

### v1/v2

#### `OrderLineSeoSerializer`

* Make `regions` optional.

## 1.4.29

### v1/v2

#### `OrderLineInAppSerializer`

* Remove INAPP_AUDIENCE_OTHER choice
* Make `target_audiences` optional. One of the `target_audiences` and `other_target_audiences` is required

## 1.4.25

### v1/v2

#### `OrderLineSerializer`

* Add new field: `payment_cycle`: choice of `PRODUCT_PAYMENT_CYCLE_CHOICES`, optional

## 1.4.24

### v1/v2

#### `OrderLineListingSerializer`

* Add two new fields: `tonline_costs` and `tonline_city`

### `PRODUCT_TYPE_CHOICES`

* Add choice `PRODUCT_TYPE_TONLINE`

## 1.4.23

### v1/v2

#### `AccountLocationSerializer`

* Add validation: required `payment_debit_account_iban` in case of `payment_type` Charge 

## 1.4.12

### v2

#### `OrderLineWebsiteSerializer`

* Added proper choices for
    * `design_preference_minimalistic_embellished`
    * `design_preference_modern_classic`
    * `design_preference_simple_striking`
    * `design_preference_text_picture`

## 1.4.10

### v1/v2

#### `OrderLineFacebookSerializer`
* `ages` choices adjustment: `14_18` is now `13_17` and `19_24` is `18_24`

## 1.4.9

### v2

#### `OrderLineWebsiteSerializer`
* Restrict validator for field `desired_domain` to accept only domain names without http protocol and no IP addresses 

## 1.4.6

### v1 / v2

#### `OrderLineGoogleAdsPremiumSerializer`
* Add optional `expected_impressions` and `expected_impression_share`

### v1

* Add optional `target_page_type`

## 1.4.5

### v1 / v2

#### `AccountLocationSerializer`
* Allow `google_places_id` to be 1000 characters max (was 30 before)

## 1.4.3

### v2

#### `OrderLineWebsiteSerializer`
* `additional_subpages` must be >= 0 and <= 60 now

#### `OrderLineGoogleAdsBasicSerializer`
* added optional `target_url`

#### `OrderLineGoogleAdsPremiumSerializer`
* added optional `target_url`

## 1.4.2

### v2

#### `AccountSerializer`
* `branch_codes` cannot be empty any more

#### `OrderLineSeoSerializer`
* `topics` cannot be empty any more
* `regions` cannot be empty any more

#### `OrderLineGoogleAdsBasicSerializer`
* `regions` cannot be empty any more

## 1.4.1

### v2

#### `OrderLineLandingpageSerializer`
added, similar to `OrderLineWebsiteSerializer` except for
* `additional_subpages`: positive integer, required
* `logo_creation`: choice of `LOGO_CREATION_CHOICES`, required

#### `OrderLineSerializer`
* added `detail_landingpage`: type `OrderLineLandingpageSerializer`, only required when OrderLine represents a landingpage product

#### `OrderLineGoogleAdsBasicSerializer`
* added `target_page_type`: choice of `GOOGLE_ADS_LANDING_PAGE_CHOICES`, optional
    * see `Serializer` changes for validation

#### `OrderLineGoogleAdsPremiumSerializer`
* added `branch_codes`: list of HeroCentral provided industry topic codes, optional
    * HeroCentral will validate the codes against the industry tree
* added `target_page_type`: choice of `GOOGLE_ADS_LANDING_PAGE_CHOICES`, optional
    * see `Serializer` changes for validation
* added `remarketing_setup_fee`: decimal, must be >=0 if `include_remarketing=true`
* added `remarketing_budget`: decimal, must be >=0 if `include_remarketing=true` 

#### Validations
* added validation: if any OrderLine detail contains `target_page_type`
    * if set to `NEW_WEBSITE`, the serializer will require an OrderLine of type `PRODUCT_TYPE_WEBSITE` to exist
    * if set to `NEW_LANDINGPAGE`, the serializer will require an OrderLine of type `PRODUCT_TYPE_LANDINGPAGE` to exist
    * OrderLine details which can provide values for `target_page_type` are: 
        * OrderLineDisplayBasicSerializer
        * OrderLineDisplayPremiumSerializer
        * OrderLineSeoSerializer
        * OrderLineInAppSerializer 
        * OrderLineFacebookSerializer
