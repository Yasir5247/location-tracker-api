# REST API Example


Base URL: [`https://locationtrace.egov.mv`].

## Using the REST API

You can access the REST API of the server using the following endpoints:

### `POST`

- `/otp/sendOtp`: Create a new post
   - Body:
      - `phoneNumber: String` (required): The mobile number
   - Response
      ```diff
         {
            success: boolean
            response: {
               id: Int
               phone_number: String
               timestamp: Date
            }
         }
      ```

- `/otp/reSendOtp`: Create a new user
   - Body:
      - `phoneNumber: String` (required): The mobile number
      - `id: Int` (optional): OTP response ID
   - Response
      ```diff
         {
            success: boolean
            response: {
               id: Int
               phone_number: String
               timestamp: Date
            }
         }
      ```

- `/otp/verifyOtp`: Create a new user
   - Body:
      - `phoneNumber: String` (required): The mobile number
      - `code: String` (optional): OTP code
   - Response
      ```diff
         {
            success: boolean
            response: {
               id: Int
               phone_number: String
               status: Int
               timestamp: Date
            }
         }
      ```

- `/app/register`: Create a new user
   - Body:
      - `name: String` (required): The name of the user
      - `registrationNumber: String` (optional): The reg number of the location
      - `phoneNumber: PostCreateInput[]` (optional): The verified mobile phone number 
   - Response
      ```diff
         data: {
            location: {
               id: Int
               phoneNumber: String
               registrationNumber: String
               updatedAt: Date 
               createdAt
            }
         }
      ```

- `/app/userEntry`: Create a new user
   - Body:
      - `locationId: Int` (required): 
      - `policePassId: Int` (optional): 
   - Response
      ```diff
         {
            success: boolean
         }
      ```


## Database Schema

```diff

model Location {
  id      Int      @default(autoincrement()) @id
  phoneNumber           String?
  registrationNumber    String   @unique
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model LocationUser {
  id              Int         @id @default(autoincrement())
  createdAt       DateTime    @default(now())
  updatedAt       DateTime    @updatedAt
  location        Location?   @relation(fields: [locationId], references: [id])
  policePassId    Int
  locationId      Int
}
```

