# Kerby-S.O.P.H.I.A._SCDFXIBM

Without reiterating too much of the short description, our team chose the problem statement titled: **Emergency Medical Services**. We have came up with a system (S.O.P.H.I.A.) where it enables real-time monitoring for early intervention measures. It is also connected to various applications from IBM technologies and relevant organizations like SCDF and other health organizations in Singapore. We understand that some of these connections or API endpoints are not available currently. For the sake of proof of concept, we will assume such technologies are present. Throughout this detailed description, we will explain the rationale behind each implementation. 

S.O.P.H.I.A. (Safety Officer Personalised Health Intelligence Assistant) is made up of three main layers:
1. Data Collection Layer
2. Data Consolidation and Cognitive Layer
3. Data Communication Layer

Analogous to the human body, the data collection layer serves as the sight and hearing function, the data consolidation and cognitive layer serves as the brain function and the data communication layer serves as the speech and movement actions. Here is a visual representation of the S.O.P.H.I.A. architecture.

![S.O.P.H.I.A. System](solution-architecture.png)

## Seeing and Hearing (Data Collection Layer)

With the advent of IoTs, we are now able to collect real-time data. The main aim of collecting real-time data is to detect irregular behavior within the household. Apart from using IoTs to collect real-time data, we can also use a chatbot to collect more qualitative data. Using natural language processing, the chatbot will be able to perceive and bring attention to important words that can alert us a potentially irregular behavior.

Detecting irregular behavior presents us with an opportunity for early intervention. 

Let us illustrate with a simple example:

Regular Scenario: Person watches TV from 10am-12pm, 1pm-5pm and 7pm-9pm daily.  
Irregular Scenario: Person progressively watches lesser TV at the regular intervals. Other utilites usage like gas (cooking) has also seen a dip. Person remarked to the chatbot that they are always tired and have minor pains around the body for an extended period of time.

Possible Explanations:
1. Person is suffering from an onset of depression, with a increase in listlessness to carry out usual activities.
2. Person had a fall/injury, inhibiting the ability to perform usual activities.

In such cases, either the Community First Responders (CFRs), a family member or a professional officer can step in to properly assess the situation and provide mitigating remedies before a high-risk event occurs. This ensures that there will be potentially lesser high-risk event related calls to the SCDF and at the same time protects the well-being of the home owner.

### Points of data collection

There are three main categories of points of data collection:
1. Utilities (IoT, quantitative data)
2. Kitchen Activity (IoT, quantitative data)
3. User Responses (Chatbot, qualitative data)

#### Utilities

Under the Utilities category, we will be observing and measuring Electricity, Gas and Water usage through IoTs. In fact, the option to have such measurements using a "smart meter" taken already exist in the market.  
(See: https://www.ema.gov.sg/Metering_Options.aspx)  

![Smart Water Meter](Smart-Water-Meter.jpg)  
(Credit: https://www.straitstimes.com/singapore/300000-smart-water-meters-to-be-installed-in-homes-firms)

Ideally, we would want to have IoTs that can measure usage from different appliances around the house for a more accurate representation of a typical behavior.

#### Kitchen Activity

Under the Kitchen Activity scategory, we will be observing and measuring Kitchen Activity through a Motion Sensor IoT. This is relevant because it help prevent fires related disasters in the household kitchen. The motion activity is to be used in tandem with the Gas usage data. 

If the gas is being utilized for 'x' amount of time and the motion sensor did not sense any movement in 'y' amount of time since the start of the gas usage, then an alarm will be triggered via IBM Watson Studio. This alarm will be sent to the chatbot via IBM Watson Assistant to alert the user.

#### User Responses via Chatbot

The envisioned end product of S.O.P.H.I.A.'s chatbot would be one that is able to dive into a deep conversation with the user and entertain them. Instead of an interrogative chatbot that would seem cold and will not elicit any useful responses from the user.

Through daily conversations with the user, the user might have instances where they mentioned about incidents that happened within their household or their general mood. The chatbot then serves as a platform to obtain vital information for early intervention.

Otherwise, without a chatbot, the user (an elderly) might have not mentioned their ailments, injuries or incidents to anyone. They might view such occurences as minor but it may come to a point where a build up such incidents will lead to an eventual high-risk incident of which it might be too late to recover from.

## Understanding and Acting (Data Consolidation and Cognitive Layer)

This is where all the data from the various sources come together to be fed into the models implemented within IBM Watson Studio.

### Double Layered AI Architecture

![Double Layered AI Architecture](double-layer-ai.jpg)

Anomaly detection models (Gas, Electricity, Water) will be implemented with a AutoEnconder Model. An example for the Eletricity utility is shown below, other utilities are similar and reserved for future work.
Kitchen Fire Risk Model, Comprehensive NLP Model and Emergency Scoring Model will be reserved for future work.

The components in the Double Layered AI Architecture are:
1. Layer 1
    1. Gas Usage Anomaly Model
    2. Electricity Usage Anomaly Model
    3. Water Usage Anomaly Model
    4. Kitchen Fire Risk Detection Model
    5. Comprehensive NLP Model
        1. Query Intent with Watson Assistant
        2. Deep Conversational Model
2. Layer 2
    1. Emergency Scoring Model
  
In Layer 1, the models will receive inputs from the IoTs/chatbot directly. Within this layer, each model will be trained on the user's own behavoiral patterns within the household. Their eventual output will be a weight/score that will serve as an input to Layer 2.

Within Layer 1, the Comprehensive NLP Model will consist of the Query Intent with Watson Assistant and a Deep Conversational Model. A portion of the Query Intent with Watson Assistant is completed within the 48 hours. However, a Deep Conversational Model is a highly complex research area which would require more resources to develop a working model.

In Layer 2, the Emergency Scoring Model will receive the outputs from Layer 1 as its input. Ideally, some form of online learning should be in place here. This allows for the Emergency Scoring Model to re-train on-the-go. The online learning will provide feedback to the model if the eventual output is a True Positive, False Positive, False Negative or True Negative.

*Due to the complexity of such implementation and the time constraint of the hackathon, the series of explanation above is not perfect and will require refinement with further research*

### Example of a Electric Usage Anomaly Detection Model

In this section we will discuss an example of a Neural Network using an AutoEncoder model to detect anomalies from Electricity Usage Data.

A machine learning algorithm on Watson Studio will receive the respective data collected from the respective IoT sensors via the IoT platform on IBM Cloud. The ML algorithm executes Anomaly Detection with respect to ‘healthy’ data of a normal / regular / day-to-day activities of the residents in a household. 
 
A baseline architecture of the ML algorithm has been built such that it performs with an accuracy of 98% regardless of the type input data (electricity, water, gas, motion). It was built based on the household power consumption dataset collected by UCI, Center of Machine Learning and Intelligent Systems. (Source: https://archive.ics.uci.edu/ml/datasets/Individual+household+electric+power+consumption)

The data is that of a one-minute sample over a period of almost 4 years. However, in view of a quick simulation of the proposed solution, only data spanning across 5 days was utilized. The 7 features used for constructing the model are as follows: 

1) Global_active_power (Household) 
2) Global_reactive power (Household) 
3) Voltage 
4) Global_intensity (Household) 
5) Sub_metering_1 (Kitchen)  
6) Sub_metering_2 (Laundry room) 
7) Sub_metering_3 (Electric water heater & air-con)

** The features are with respect to the household power consumption dataset from UCI. It was only used for simulation purposes in this case. In view of deployment with Singapore households, the respective data will need to be collected from the relevant authorities. As such, number of features may vary as per the availability of data.

The architecture, known as an Autoencoder, is as follows:

![AutoEncoder Architecture](AE-Architecture.jpg)


The aim of the AE is to reproduce the same input data as the output and calculate the respective cost function. Therefore, it will only be trained on the ‘healthy’ (normal/ regular/ day-day) activities of the household such as electricity usage, water usage, gas usage and motion within the house. 

The accuracy of the model trained with electricity consumption data after 100 epochs is shown as follows:

![AutoEncoder Results](AE-Results.png)

A threshold is built based of the mean squared error (MSE) produced from training the AE with only the data of ‘healthy’ (normal/ regular/day-to-day) activities. 

![AutoEncoder MSE](AE-Mse.png)
 
Any deviation from the threshold indicates an anomalous activity. The activity can be a spike in electricity usage which might indicate the onset of a potential circuitry damage and fire or it can be a prolonged usage of gas which might indicate that it was left unattended for long.


## Communicating (Data Communication Layer)

Data will be communicated to two parties: The User and The Analytics Team.
The two parties will see different forms of data. The User will primarily consume data in the form of the Chatbot responses, where the Chatbot will furnish relevant information retrieved from IBM Watson Discovery as a form of early assistance. The Analytics Team will monitor the readings from a particular user or a group of users.

The main goal of the analytics team is to study the data and deliver insights for improvements in the models, chatbot and crisis/pre-crisis handling procedure.

### Chatbot
text-to-speech
speech-to-text
multi-lingual

blank blank

#### Function #1: Deep Conversation
#### Function #2: Query Intent
watson discovery
#### Function #3: Providing 


## Overview

| Completed during the Hackathon | Not Completed |
|:---:|:---:|
| Electricity Usage Anomaly Model | Gas Usage Anomaly Model |
| Query Intent with Watson Assistant | Water Usage Anomaly Model |
|   | Kitchen Fire Risk Detection Model |
|   | Deep Conversational Model |
|   | Emergency Scoring Model |
|   | Monitoring Dashboard Web Application |
|   | Chatbot Mobile Application |

## Conclusion 

S.O.P.H.I.A. is not meant to be a surveillance system, its purely meant to enable safer living by identifying early intervention opportunities. The bulk of the difficulty in implementing S.O.P.H.I.A. lies in the developing the deep conversational model for the chatbot. Being able to identify early intervention opportunities and to steer the user toward the proper relief measure will reduce the amount of operating workload for SCDF. S.O.P.H.I.A. is a step toward transforming Singapore into a smart nation.  

### Future Work

Developing the chatbot to ensure safe living requires advice from subject matter experts in several fields:
1) Medical Officers: Give insights on how to properly advise in any injury event, identifying patterns in symptoms that may lead up to a high risk event
2) Social Workers: How to engage the elderly, special areas to look out for when communicating with the elderly
3) Psychologist: Identify patterns in mood swings, providing proper responses and questions to the user


