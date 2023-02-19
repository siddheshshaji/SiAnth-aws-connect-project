# AWS Connect Project
Automated call center using AWS Connect, Glue, Lambda, Athena, S3 and Quicksight


The Flow:

1. There are 4 members in the hardcoded database with attributes: name, phone number, member id number, dob, address, zip and possible intent

1. When a cusomer calls the customer care number, a prompt is played that says:

"Thanks for calling {i don't recall the name of your firm, please let me know} helpline.
Press 1 to connect with the Human Resources Department.
Press 2 to connect with the Information Technology Department.
Press 3 to connect with the Marketing Department.
Press 4 to connect with the Sales Department."

After the caller enters an option, we capture two attributes,
- customer_number (customer mobile number)
- customer_choice (1,2,3 or 4) 

3. Then, customer_choice is verified for being one among 1,2,3 or 4, if not, a prompt says "Sorry, that's not a valid option, try again." and we go back to point 2. Otherwise, a lambda function searchMemberByPhone is invoked which searches whether customer_number matches with any phone number in the hardcoded database records.

4. If customer_number is present, a prompt says "Welcome {customer_name} are you trying to enquire about {possible_intent}, if yes, press 1, else press 2." 

	4.1 If the caller presses 1, the hardcoded intent is read out 
	4.2 If they press 2, a prompt says "Ok, I will connect you to a marketing(for eg. if the 			customer_choice was 3) representative now."
	4.3 Any other number invokes a "Sorry that's not a valid option, try again." prompt and takes 	it back to 4

5. If customer_number is not present in the database, a prompt says "We don't have your profile or your phone number registered in our records, if you are an existing customer, please press 1, else press 0." 

	5.1 If the caller presses 1, we have a series of three prompts asking for their member id, birth 	year and zip code and a lambda function searchMemberByMiscellaneous is invoked which 		checks whether the entered combination is correct, if it is correct, we go to point 4. If it is 		incorrect, we go back to point 5(expecting the caller to press 0)
	5.2 If the caller presses 0, we go back to point 4.2
	5.3 Any other number invokes a "Sorry that's not a valid option, try again." prompt
  


AWS Flowchart for Quicksight Analytics

![image](https://user-images.githubusercontent.com/62932933/219936837-e79e24b2-6870-4dbf-bc79-9c9a3055ee4b.png)
