# Termii Node Library

[![Made in Nigeria](https://img.shields.io/badge/made%20in-nigeria-008751.svg?style=flat-square)](https://github.com/acekyd/made-in-nigeria)
![npm (scoped)](https://img.shields.io/npm/v/@termii/node?color=%23FF7B37&style=flat-square)
![npm](https://img.shields.io/npm/dm/@termii/node?style=flat-square)
![Twitter Follow](https://img.shields.io/twitter/follow/eminisolomon?style=social)

Nodejs SDK for [Termii](https://termii.com) messaging platform written in typescript

## Table of content

- [Prerequisites](#prerequisites)
- [Getting started](#getting-started)
- [Installation](#installation)
- [Usage](#usage)
- [Available Services exposed by the SDK](#available-services-exposed-by-the-sdk)
  - [Sender ID](#sender-id)
    - [Fetch Sender ID](#fetch-sender-id)
    - [Create Sender ID](#create-sender-id)
  - [Messaging](#messaging)
    - [Send Message](#send-message)
    - [Send Bulk Message](#send-bulk-message)
  - [Number](#number)
    - [Send Message with Number](#send-message-with-number)
- [License](#license)

## Prerequisites

Node v16 and higher is required. To make sure you have them available on your machine, try running the following command.

```sh
 node -v
```

## Getting Started

To get started with this SDK, create an account on [Termii](https://accounts.termii.com/#/register) if you haven't already.
You can then retrieve your API keys from your Termii dashboard.

## Installation

This SDK can be installed with npm or yarn or pnpm.

```sh
# using npm
npm install @termii/node
# using yarn
yarn install @termii/node
# using pnpm
pnpm add @termii/node
```

## Usage

Import and Initialize the library

```ts
// use modules
import { Termii } from '@termii/node';
// use cjs
const { Termii } = require('@termii/node')

const termii = new Termii('YOUR_API_KEY');
```

Instantiate the Termii class

```ts
const termii = new Termii('YOUR_API_KEY');
```

> **Warning**
Be sure to keep your API Credentials securely in environment variables.

## Available Services exposed by the SDK

### Sender ID API

A Sender ID is the name or number that identifies the sender of an SMS message.

#### Fetch Sender ID

```ts
// import the sender id response interface from the sdk
import { ISenderIDResponse } from '@termii/node';

// returns the first 15 sender ids
const senderIds = await termii.message.fetchSenderIDs()

// to get the next page of sender ids 
const senderIds = await termii.message.fetchSenderIDs(2)
console.log(senderIds) // ISenderIDResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/sender-id#fetch-sender-id)

#### Create Sender ID

```ts
// import the request sender id interfaces from the sdk
import { IRequestSenderID, IRequestSenderIDResponse } from '@termii/node';

const payload: IRequestSenderID = {
  sender_id: 'acme',
  usecase: 'Testing! Working!! This is it!!!',
  company: 'Metalabs',
}

const response = await termii.message.requestSenderID(payload)
console.log(response) // IRequestSenderIDResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/sender-id#request-sender-id)

### Messaging API

This API allows businesses send text messages to their customers across different messaging channels.

#### Send Message

```ts
// import the message interfaces from the sdk
import { ISendMessage, ISendMessageResponse } from '@termii/node';

const payload: ISendMessage = {
  to: "2347880234567",
  from: "talert",
  sms: "Hi there, testing Termii",
  type: "plain",
  channel: "generic",
  api_key: "Your API Key",
  media: {
    url: "https://media.example.com/file",
    caption: "your media file"
  }    
}

const response = await termii.message.sendMessage(payload)
console.log(response) // ISendMessageResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/messaging-api#send-message)

#### Send Bulk Message

```ts
// import the message interfaces from the sdk
import { ISendBulkMessage, ISendBulkMessageResponse } from '@termii/node';

const payload: ISendBulkMessage = {
  to: ["23490555546", "23423490126999","23490555546"],
  from: "talert",
  sms: "Hi there, testing Termii",
  type: "plain",
  channel: "generic"
}

const response = await termii.message.sendBulkMessage(payload)
console.log(response) // ISendBulkMessageResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/messaging-api#send-bulk-message)

### Number API

This allows businesses send messages to customers using Termii's auto-generated messaging numbers that adapt to customers location.

#### Send Message with Number

```ts
// import the number interfaces from the sdk
import { ISendMessageWithNumber, ISendMessageWithNumberResponse } from '@termii/node';

const payload: ISendMessage = {
  to: "23490555546",
  sms: "Hi there, testing Termii"
}

const response = await termii.message.sendMessageWithNumber(payload)
console.log(response) // ISendMessageWithNumberResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/number#send-message)

### Templates API

This helps businesses set a template for the one-time-passwords (pins) sent to their customers via whatsapp or sms.

#### Device Template (Send Message with Template)

```ts
// import the template interfaces from the sdk
import { IDeviceTemplate, IDeviceTemplateResponse } from '@termii/node';

const payload: IDeviceTemplate = {
  phone_number: '+1234567890',
  device_id: 'device123',
  template_id: 'template456',
  data: {
    product_name: 'Dummy Product',
    otp: 123456,
    expiry_time: '2023-11-16T12:00:00Z',
  },
}

const response = await termii.message.sendMessageWithTemplate(payload)
console.log(response) // IDeviceTemplateResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/templates#device-template)

### Phonebooks

Create, view & manage phonebooks using these APIs. Each phonebook can be identified by a unique ID, which makes it easier to edit or delete a phonebook.

#### Fetch Phonebooks

```ts
// import the phonebook interfaces from the sdk
import { IFetchPhonebooksResponse } from '@termii/node';

const response = await termii.message.fetchPhonebooks()

// to fetch another page - pass the page number to the method
const response = await termii.message.fetchPhonebooks(2)
console.log(response) // IFetchPhonebooksResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/phonebook#fetch-phonebooks)

#### Create Phonebook

```ts
// import the phonebook interfaces from the sdk
import { IPhonebookResponse, IPhonebook, } from '@termii/node';

const payload: IPhonebook = {
  phonebook_name: 'Test',
  description: 'Phonebook for test',
}

const response = await termii.message.createPhonebook(payload)
console.log(response) // IPhonebookResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/phonebook#create--a-phonebook)

#### Update Phonebook

```ts
// import the phonebook interfaces from the sdk
import { IPhonebookResponse, IPhonebook, } from '@termii/node';

const payload: IPhonebook = {
  phonebook_name: 'Update testTest',
  description: 'Updated Phonebook for test',
}

const response = await termii.message.updatePhonebook('phonebook_id', payload)
console.log(response) // IPhonebookResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/phonebook#update-phonebook)

#### Delete Phonebook

```ts
// import the phonebook interfaces from the sdk
import { IPhonebookResponse } from '@termii/node';

const response = await termii.message.deletePhonebook('phonebook_id')
console.log(response) // IPhonebookResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/phonebook#delete-phonebook)

### Contacts

Contacts API allows you manage (i.e. edit, update, & delete) contacts in your phonebook.

#### Fetch contacts by phonebook ID

```ts
// import the contact interfaces from the sdk
import { IFetchContactsResponse } from '@termii/node';

const response = await termii.message.fetchContacts('phonebook_id')

// to fetch another page - pass the page number to the method after the phonebook ID
const response = await termii.message.fetchContacts('phonebook_id', 2)
console.log(response) // IFetchContactsResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/contacts#fetch-contacts-by-phonebook-id)

#### Add single contacts to phonebook

```ts
// import the contact interfaces from the sdk
import { ICreateContact, ICreateContactResponse } from '@termii/node';

const payload: ICreateContact = {
  phone_number: '8123696237',
  email_address: 'test@gmail.com',
  first_name: 'test',
  last_name: 'contact',
  company: 'Termii',
  country_code: '234',
}

const response = await termii.message.createContact('phonebook_id', payload)
console.log(response) // ICreateContactResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/contacts#add-single-contacts-to-phonebook)

#### Delete contact

```ts
// import the contact interfaces from the sdk
import { IDeleteContactResponse } from '@termii/node';

const response = await termii.message.deleteContact('contact_id')
console.log(response) // IDeleteContactResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/contacts#delete-phonebook)

### Campaign

Using the campaign APIs, you can view, manage and send a campaign to a phonebook.

#### Fetch campaigns

```ts
// import the campaign interfaces from the sdk
import { IFetchCampaignsResponse } from '@termii/node';

const response = await termii.message.fetchCampaigns()

// to fetch another page - pass the page number to the method
const response = await termii.message.fetchCampaigns(2)
console.log(response) // IFetchCampaignsResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/campaign#fetch-campaigns)

#### Fetch campaign history

```ts
// import the campaign interfaces from the sdk
import { fetchCampaignHistoryResponseData } from '@termii/node';

const response = await termii.message.fetchCampaigns('campaign_id')

// to fetch another page - pass the page number to the method after campaign ID
const response = await termii.message.fetchCampaigns('campaign_id', 2)
console.log(response) // fetchCampaignHistoryResponseData
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/campaign#fetch-campaign-history)

#### Send a campaign

```ts
// import the campaign interfaces from the sdk
import { ISendCampaign, ISendCampaignResponse } from '@termii/node';

const payload: ISendCampaign = {
  api_key: "Your API KEY",
  country_code: "234",
  sender_id: "Termii",
  message: "Welcome to Termii.",
  channel: "generic",
  message_type: "Plain",
  phonebook_id: "2d9f4a02-85b8-45e5-9f5b-30f93ef472e2",
  delimiter: ",",
  remove_duplicate: "yes",
  campaign_type: "personalized",
  schedule_time: "30-06-2021 6:00",
  schedule_sms_status: "scheduled"
}

const response = await termii.message.sendCampaign(payload)

console.log(response) // ISendCampaignResponse
```

Find more details about the parameters and response for the above method [here](https://developers.termii.com/campaign#send-a-campaign)


## License

[MIT](https://github.com/peoray/@termii/node/blob/main/LICENSE)
