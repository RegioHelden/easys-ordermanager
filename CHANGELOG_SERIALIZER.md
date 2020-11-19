# Serializer changes

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
