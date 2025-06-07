# Color Module

This document provides a detailed guide to the Color module, focusing on the Color model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### Color

Defines the structure for colors.

```typescript
type Color = {
  color: string;
  name: string;
};
```

### CreateColorDTO

Defines the structure for creating a color.

```typescript
type CreateColorDTO = {
  color: string;
  name: string;
  external_id?: any;
};
```

### UpdateColorDTO

Defines the structure for updating a color.

```typescript
type UpdateColorDTO = {
  color?: string;
  name?: string;
};
```

## Example Usage

### Create a Color

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateColorDTO } from './Color'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newColorData = { // CreateColorDTO type assumed to be available
  color: '#FFFFFF',
  name: 'White',
  // external_id is optional
};

sdk.color.create(newColorData).then((color) => {
  console.log('Color created:', color);
});
```
Response example:
```json
{
  "_id": "colorId123",
  "color": "#FFFFFF",
  "name": "White",
  "external_id": null,
  "createdAt": "2023-10-28T15:00:00.000Z",
  "updatedAt": "2023-10-28T15:00:00.000Z",
  "id": "colorId123"
}
```

### Update a Color

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateColorDTO } from './Color'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateColorData = { // UpdateColorDTO type assumed to be available
  name: 'Bright White',
};

sdk.color.updateById('colorId', updateColorData).then(() => {
  console.log('Color updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching colors

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.color.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('color:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "colorId123",
      "color": "#FF0000",
      "name": "Red",
      "external_id": null,
      "createdAt": "2023-10-28T15:00:00.000Z",
      "updatedAt": "2023-10-28T15:05:00.000Z",
      "id": "colorId123"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a color by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.color.findById('colorId').then((color) => {
  console.log('color:', color);
});
```
Response example:
```json
{
  "_id": "colorId123",
  "color": "#0000FF",
  "name": "Blue",
  "external_id": "ext-blue-001",
  "createdAt": "2023-10-28T15:10:00.000Z",
  "updatedAt": "2023-10-28T15:10:00.000Z",
  "id": "colorId123"
}
```

### Deleting a color

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.color.deleteById('colorId').then(() => {
  console.log('color deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```