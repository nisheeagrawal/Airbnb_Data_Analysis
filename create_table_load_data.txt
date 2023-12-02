CREATE SCHEMA IF NOT EXISTS da_airbnb

CREATE TABLE IF NOT EXISTS da_airbnb.calendar (
	listing_id BIGINT,
	date DATE,
	available TEXT,
	price TEXT
  )

	CREATE TABLE IF NOT EXISTS da_airbnb.listings (
	  	id INT,
	  	listing_url VARCHAR,
	  	scrape_id BIGINT,
	  	last_scraped DATE,
	  	name VARCHAR,
	  	summary TEXT,
	  	space TEXT,
	  	description TEXT,
	  	experiences_offered TEXT,
	  	neighborhood_overview TEXT,
	  	notes TEXT,
	  	transit TEXT,
	  	thumbnail_url VARCHAR,
	  	medium_url VARCHAR,
	  	picture_url VARCHAR,
	  	xl_picture_url VARCHAR,
	  	host_id BIGINT,
	  	host_url VARCHAR,
	  	host_name VARCHAR,
	  	host_since DATE,
	  	host_location VARCHAR,
	  	host_about TEXT,
	  	host_response_time VARCHAR,
	  	host_response_rate VARCHAR,
	  	host_acceptance_rate VARCHAR,
	  	host_is_superhost TEXT,
	  	host_thumbnail_url VARCHAR,
	  	host_picture_url VARCHAR,
	  	host_neighbourhood TEXT,
	  	host_listings_count INT,
	  	host_total_listings_count INT,
	  	host_verifications TEXT,
	  	host_has_profile_pic TEXT,
	  	host_identity_verified TEXT,
	  	street VARCHAR,
	  	neighbourhood TEXT,
	  	neighbourhood_cleansed TEXT,
	  	neighbourhood_group_cleansed TEXT,
	  	city TEXT,
	  	state TEXT,
	  	zipcode INT,
	  	market TEXT,
	  	smart_location VARCHAR,
	  	country_code TEXT,
	  	country TEXT,
	  	latitude DECIMAL,
	  	longitude DECIMAL,
	  	is_location_exact TEXT,
	  	property_type TEXT,
	  	room_type VARCHAR,
	  	accommodates INT,
	  	bathrooms DECIMAL,
	  	bedrooms INT,
	  	beds INT,
	  	bed_type TEXT,
	  	amenities VARCHAR,
	  	square_feet INT,
	  	price TEXT,
	  	weekly_price TEXT,
	  	monthly_price TEXT,
	  	security_deposit TEXT,
	  	cleaning_fee TEXT,
	    guests_included INT,
	    extra_people TEXT,
	    minimum_nights INT,
	    maximum_nights INT,
	    calendar_updated TEXT,
	    has_availability TEXT,
	    availability_30 INT,
	    availability_60 INT,
	    availability_90 INT,
	    availability_365 INT,
	    calendar_last_scraped DATE,
	    number_of_reviews INT,
	    first_review DATE,
	    last_review DATE,
	    review_scores_rating INT,
	    review_scores_accuracy INT,
	    review_scores_cleanliness INT,
	    review_scores_checkin INT,
	    review_scores_communication INT,
	    review_scores_location TEXT,  -- Missing from original version of the file
	    review_scores_value INT,
	    requires_license TEXT,
	    license BIT,
	    jurisdiction_names TEXT,
	    instant_bookable TEXT,
	    cancellation_policy TEXT,
	    require_guest_profile_picture TEXT,
	    require_guest_phone_verification TEXT,
	    calculated_host_listings_count INT,
	    reviews_per_month DECIMAL
	    );

CREATE TABLE IF NOT EXISTS da_airbnb.listings (
    listing_id BIGINT,
    id INT,
    date DATE,
    reviewer_id BIGINT,
    reviewer_name TEXT,
    comments TEXT
)

DELETE FROM da_airbnb.calendar
DELETE FROM da_airbnb.listings
DELETE FROM da_airbnb.reviews

COPY da_airbnb.calendar(listing_id, date, available, price)
FROM '/tmp/calendar.csv'
DELIMITER ','
CSV HEADER

COPY da_airbnb.listings(id, listing_url, scrape_id, last_scraped, name, summary, space, description, experiences_offered, neighborhood_overview, notes, transit, thumbnail_url, medium_url, picture_url, xl_picture_url, host_id, host_url, host_name, host_since, host_location, host_about, host_response_time, host_response_rate, host_acceptance_rate, host_is_superhost, host_thumbnail_url, host_picture_url, host_neighbourhood, host_listings_count, host_total_listings_count, host_verifications, host_has_profile_pic, host_identity_verified, street, neighbourhood, neighbourhood_cleansed, neighbourhood_group_cleansed, city, state, zipcode, market, smart_location, country_code, country, latitude, longitude, is_location_exact, property_type, room_type, accommodates, bathrooms, bedrooms, beds, bed_type, amenities, square_feet, price, weekly_price, monthly_price, security_deposit, cleaning_fee, guests_included, extra_people, minimum_nights, maximum_nights, calendar_updated, has_availability, availability_30, availability_60, availability_90, availability_365, calendar_last_scraped, number_of_reviews, first_review, last_review, review_scores_rating, review_scores_accuracy, review_scores_cleanliness, review_scores_checkin, review_scores_communication, review_scores_location, review_scores_value, requires_license, license, jurisdiction_names, instant_bookable, cancellation_policy, require_guest_profile_picture, require_guest_phone_verification, calculated_host_listings_count, reviews_per_month)
FROM '/tmp/listings.csv'
DELIMITER ','
CSV HEADER;

COPY da_airbnb.reviews(listing_id, id, date, reviewer_id, reviewer_name, comments)
FROM '/tmp/reviews.csv'
DELIMITER ','
CSV HEADER
