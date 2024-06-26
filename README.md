Travel App - README Template
Travel Recommendation App
Table of Contents
Overview
Product Spec
-  
Wireframes
Schema
Overview
Description
- This app will allow for a user to set preferences such as age, interests(ex. history or nightlife). Once the user sets their preferences the app will suggest different types of attractions that meet the specific guidlines that the user has set. They will be able to choose for different attractions in their area and rate them on a scale of 1-5.There will also be a feature that allows users to discuss and offer suggestions on where to go and all tourst related information.  

App Evaluation
   - **Description**:  This app will allow for a user to set preferences such as age, interests(ex. history or nightlife). Once the user sets their preferences the app will suggest different types of attractions that meet the specific guidlines that the user has set. They will be able to choose for different attractions in their area and rate them on a scale of 1-5. There will also be a feature that allows users to discuss and offer suggestions on where to go and all tourst related information.
  
   - **Category:** Tourism
    
   - **Mobile:** Mobile is essential for the instant access to things such as tickets and directions. Users can use the app to purchase tickets from the recommended attractions tab. The camera is used to share images with that may be used for uploading reviews.
   
   - **Story:** Allows travelers to find attractions based off their personal interest that would not have been found surfing the internet or blogs. 
   
   - **Market:** This application can be used by anyone searching for tourist attractions or even events or measuems near them they may have never found. This market is constantly expanding as toursim is ever so growing industry. 
  
   - **Habit:** While users are limited on their tourism. There are groups of people who are traveling very often who may use this app daily. Some of these people include Study Abroad students, people who work in airline industries, cruiseline employees, etc. 
   
   - **Scope:** V1 would allow users to find attractions near them that they feel align with their interests. There will be a way for users to enter in their interests and hobbies that may be more appelaing to them, and the app will suggest attractions they may find interesting. 
  
1. User Stories (Required and Optional)

- User Profile Creation: Allow users to create profiles where they can set preferences such as age, interests, and hobbies.
- Attractions Recommendations: Provide personalized recommendations for attractions based on user preferences.
- Attractions Information: Display detailed information about each attraction, including descriptions, opening hours, and location.
- Ratings and Reviews: Enable users to rate attractions on a scale of 1-5 and leave reviews.
- Ticket Purchasing: Integrate a feature for users to purchase tickets directly through the app for recommended attractions.
- Search Functionality: Implement a search feature for users to find attractions based on location or keywords.
- Image Sharing: Allow users to upload images of attractions and share them within the app.

Optional Nice-to-have Stories
- Social Sharing: Enable users to share their experiences and recommendations on social media platforms.
- Event Recommendations: Expand beyond attractions to include recommendations for local events and festivals.
- Offline Access: Provide offline access to attraction information and directions for users traveling in areas with limited connectivity.
- Language Support: Offer support for multiple languages to cater to international users.
- Customizable Notifications: Allow users to customize notifications for updates on new attractions or events matching their preferences.

2. Screen Archetypes
- Welcome/Onboarding Screen
- User Profile Creation
- Home Screen (Attraction Recommendations)
- Attractions Detail Screen
- Ratings and Reviews Screen
- Ticket Purchase Screen
- Search Screen
- Image Sharing Screen
- Settings Screen

3. Navigation
- User opens the app
- Welcome/Onboarding Screen is displayed
- User proceeds to create a profile or log in
- After profile creation, user is directed to the Home Screen
- Home Screen displays personalized attraction recommendations
- User can browse attractions or use the search function
- Upon selecting an attraction, user is taken to the Attractions Detail Screen for more information
- From the detail screen, user can leave ratings and reviews, purchase tickets, or share images
- User can navigate back to the Home Screen or access other features through the navigation menu in the app.


Wireframes
https://raw.githubusercontent.com/timmesc/Travel-App/main/IMG_0278.HEIC


Video
https://youtu.be/rde6bwoq3Rs

Progress
- Currently have linked the api and am able to show locations with suggested toursit locations

[BONUS] Digital Wireframes & Mockups
[BONUS] Interactive Prototype
Schema

Please copy and paste these two links for updated wirefram and new app feature

file:///Users/charlestimmes/Desktop/Screenshot%202024-04-23%20at%201.59.42%E2%80%AFAM.png

file:///Users/charlestimmes/Desktop/Screenshot%202024-04-23%20at%201.56.33%E2%80%AFAM.png

Final Update 

https://youtu.be/rde6bwoq3Rs

Update includes:
tab bar
settings
preferences
chat room view controller

issues:
API connections 




Models

 struct Location: Codable {
        let location: String
        let attraction: String
    }
    
    enum LocationError: Error {
        case invalidResponse
    }
    

Networking

    func getLocation() async throws -> [Location] {
        let endpoint = "http://localhost:9080/location"
        
        guard let url = URL(string: endpoint) else {
            throw LocationError.invalidResponse
        }
        
        do {
            let (data, response) = try await URLSession.shared.data(from: url)
            
            guard let httpResponse = response as? HTTPURLResponse, httpResponse.statusCode == 200 else {
                throw LocationError.invalidResponse
            }
            
            let decoder = JSONDecoder()
            decoder.keyDecodingStrategy = .convertFromSnakeCase
            let locations = try decoder.decode([Location].self, from: data)
            return locations
        } catch {
            throw LocationError.invalidResponse
        }
    }
[OPTIONAL: List endpoints if using existing API such as Yelp]
