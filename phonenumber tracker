import phonenumbers
from phonenumbers import geocoder, carrier, timezone
from opencage.geocoder import OpenCageGeocode
import folium

# Step 1: Get input from user
number = input("Enter phone number with country code (e.g., +911234567890): ")

# Step 2: Parse the number
parsed_number = phonenumbers.parse(number)

# Step 3: Get details
country = geocoder.description_for_number(parsed_number, "en")
service_provider = carrier.name_for_number(parsed_number, "en")
time_zones = timezone.time_zones_for_number(parsed_number)

print("\n Phone Number Details:")
print(f"Country/Region: {country}")
print(f"Carrier: {service_provider}")
print(f"Time Zone(s): {time_zones}")

# Step 4: Get coordinates using OpenCage API
key = "4cc40d91a30444fabce9c58c6d6a6868"  # replace with your actual API key
geocoder_api = OpenCageGeocode(key)
results = geocoder_api.geocode(country)

if results:
    lat = results[0]['geometry']['lat']
    lng = results[0]['geometry']['lng']
    print(f"Latitude: {lat}, Longitude: {lng}")

    # Step 5: Create map
    map_location = folium.Map(location=[lat, lng], zoom_start=7)
    folium.Marker([lat, lng], popup=country).add_to(map_location)
    map_location.save("number_location.html")

    print("\n Map saved as number_location.html — open it to see location!")
else:
    print(" Could not find location. Check number or API key.")
