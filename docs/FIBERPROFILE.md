# FiberProfile Module

This document provides a concise guide to the FiberProfile module, focusing on the FiberProfile model and its Data Transfer Objects (DTOs) for create and update operations.

## Models

### FiberProfile

Defines the structure for a fiber profile.

```typescript
type FiberProfile = {
  id: string;
  name: string;
  defaultFiberColor: string;
  defaultTubeColor: string;
  fibers: { color: string }[];
  tubes: { color: string }[];
  external_id?: any;
};
```

### CreateFiberProfileDTO

Defines the structure for creating a fiber profile.

```typescript
type CreateFiberProfileDTO = {
  name: string; // Changed to required
  defaultFiberColor?: string;
  defaultTubeColor?: string;
  fibers: { color: string }[]; // Changed to required
  tubes: { color: string }[]; // Changed to required
  external_id?: any;
};
```

### UpdateFiberProfileDTO

Defines the structure for updating a fiber profile.

```typescript
type UpdateFiberProfileDTO = {
  name?: string;
  defaultFiberColor?: string;
  defaultTubeColor?: string;
  fibers?: { color: string }[];
  tubes?: { color: string }[];
  external_id?: any;
};
```

## Example Usage

### Creating a FiberProfile

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateFiberProfileDTO } from './FiberProfile'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const createFiberProfileData = { // CreateFiberProfileDTO type assumed to be available
  name: 'Standard 12-Fiber Profile',
  defaultFiberColor: 'blue', // Optional, will use Zod default if not provided
  defaultTubeColor: 'white', // Optional, will use Zod default if not provided
  fibers: [
    { color: 'blue' }, { color: 'orange' }, { color: 'green' }, { color: 'brown' },
    { color: 'slate' }, { color: 'white' }, { color: 'red' }, { color: 'black' },
    { color: 'yellow' }, { color: 'violet' }, { color: 'rose' }, { color: 'aqua' }
  ],
  tubes: [ { color: 'blue' }, { color: 'orange' } ], // Example for a 2-tube cable profile
  // external_id is optional
};

sdk.fiberProfile.create(createFiberProfileData).then((fiberProfile) => {
  console.log('FiberProfile created:', fiberProfile);
});
```
Response example:
```json
{
  "_id": "fpId123",
  "name": "Standard 12-Fiber Profile",
  "defaultFiberColor": "blue",
  "defaultTubeColor": "white",
  "fibers": [
    { "color": "blue" }, { "color": "orange" }, { "color": "green" }, { "color": "brown" },
    { "color": "slate" }, { "color": "white" }, { "color": "red" }, { "color": "black" },
    { "color": "yellow" }, { "color": "violet" }, { "color": "rose" }, { "color": "aqua" }
  ],
  "tubes": [ { "color": "blue" }, { "color": "orange" } ],
  "external_id": null,
  "createdAt": "2023-10-30T14:00:00.000Z",
  "updatedAt": "2023-10-30T14:00:00.000Z",
  "id": "fpId123"
}
```

### Updating a FiberProfile

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateFiberProfileDTO } from './FiberProfile'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateFiberProfileData = { // UpdateFiberProfileDTO type assumed to be available
  defaultFiberColor: 'aqua', // Changed default fiber color
  name: "Standard 12-Fiber Profile (Aqua Default)"
};

sdk.fiberProfile.updateById('fiberProfileId', updateFiberProfileData).then(() => {
  console.log('FiberProfile updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching FiberProfiles

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.fiberProfile.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('FiberProfiles:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "fpId123",
      "name": "Standard 12-Fiber Profile (Aqua Default)",
      "defaultFiberColor": "aqua",
      "defaultTubeColor": "white",
      "fibers": [
        { "color": "blue" }, { "color": "orange" }, { "color": "green" }, { "color": "brown" },
        { "color": "slate" }, { "color": "white" }, { "color": "red" }, { "color": "black" },
        { "color": "yellow" }, { "color": "violet" }, { "color": "rose" }, { "color": "aqua" }
      ],
      "tubes": [ { "color": "blue" }, { "color": "orange" } ],
      "external_id": null,
      "createdAt": "2023-10-30T14:00:00.000Z",
      "updatedAt": "2023-10-30T14:05:00.000Z", // Assuming updated
      "id": "fpId123"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a FiberProfile by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.fiberProfile.findById('fiberProfileId').then((fiberProfile) => {
  console.log('FiberProfile:', fiberProfile);
});
```
Response example:
```json
{
  "_id": "fpId123",
  "name": "Standard 12-Fiber Profile (Aqua Default)",
  "defaultFiberColor": "aqua",
  "defaultTubeColor": "white",
  "fibers": [
    { "color": "blue" }, { "color": "orange" }, { "color": "green" }, { "color": "brown" },
    { "color": "slate" }, { "color": "white" }, { "color": "red" }, { "color": "black" },
    { "color": "yellow" }, { "color": "violet" }, { "color": "rose" }, { "color": "aqua" }
  ],
  "tubes": [ { "color": "blue" }, { "color": "orange" } ],
  "external_id": "ext-fp-001",
  "createdAt": "2023-10-30T14:00:00.000Z",
  "updatedAt": "2023-10-30T14:05:00.000Z",
  "id": "fpId123"
}
```

### Deleting a FiberProfile

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.fiberProfile.deleteById('fiberProfileId').then(() => {
  console.log('FiberProfile deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```