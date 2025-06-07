# Duct Module

This document provides a concise guide to the Duct module, focusing on the Duct model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### Duct

Defines the structure for ducts.

```typescript
type Duct = {
  id: string;
  name: string;
  observation?: string;
  implanted: boolean;
  project: string;
  ductType: string;
  color?: string;
  length: number;
  edgeA: string;
  edgeB: string;
  shared: boolean;
  immediateParent?: string | Duct;
  parent?: string | Duct;
  points: string[];
  tags: string[];
  index: number;
  typeColor: {
    regular: string;
    notImplanted: string;
  };
  external_id?: any;
  // subDucts is primarily a creation/update parameter, not directly on the resolved model always
};
```

### CreateDuctDTO

Defines the structure for creating a duct.

```typescript
type CreateDuctDTO = {
  name?: string;
  observation?: string;
  implanted?: boolean;
  project: string;
  ductType: string;
  color?: string;
  edgeA: string;
  edgeB: string;
  shared?: boolean;
  points: string[];
  tags: string[];
  external_id?: any;
  subDucts?: SubDuctStructure[];
};
```

### UpdateDuctDTO

Defines the structure for updating a duct.

```typescript
type UpdateDuctDTO = {
  name?: string;
  observation?: string;
  implanted?: boolean;
  project?: string;
  ductType?: string;
  color?: string;
  length?: number;
  edgeA?: string;
  edgeB?: string;
  shared?: boolean;
  immediateParent?: string;
  parent?: string;
  points?: string[];
  tags?: string[];
  index?: number;
  typeColor?: {
    regular?: string;
    notImplanted?: string;
  };
  external_id?: any;
};
```

## Example Usage

### Creating a Duct

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateDuctDTO } from './Duct'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newDuctData = { // CreateDuctDTO type assumed to be available
  name: "Main Duct Run A-B",
  project: "projectId123",
  ductType: "ductTypeIdXYZ",
  edgeA: "junctionBoxIdA",
  edgeB: "junctionBoxIdB",
  points: ["pointId1", "pointId2", "pointId3"], // Geo-coordinates or Point entity IDs
  tags: ["core-network", "phase1"],
  implanted: true, // Optional, defaults to true
  observation: "Primary duct line along Main Street.", // Optional
  // color, shared, external_id, subDucts are optional
};

sdk.duct.create(newDuctData).then((duct) => {
  console.log('Duct created:', duct);
});
```
Response example:
```json
{
  "_id": "ductIdABC",
  "name": "Main Duct Run A-B",
  "project": "projectId123",
  "ductType": "ductTypeIdXYZ",
  "edgeA": "junctionBoxIdA",
  "edgeB": "junctionBoxIdB",
  "points": ["pointId1", "pointId2", "pointId3"],
  "tags": ["core-network", "phase1"],
  "implanted": true,
  "observation": "Primary duct line along Main Street.",
  "color": null,
  "shared": false,
  "length": 150.75, // Calculated on backend
  "immediateParent": null,
  "parent": null,
  "index": 1, // Calculated on backend
  "typeColor": { "regular": "#FF5733", "notImplanted": "#FFC300" }, // From DuctType
  "external_id": null,
  "createdAt": "2023-10-30T10:00:00.000Z",
  "updatedAt": "2023-10-30T10:00:00.000Z",
  "id": "ductIdABC"
}
```

### Updating a Duct

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateDuctDTO } from './Duct'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateDuctData = { // UpdateDuctDTO type assumed to be available
  name: "Main Duct Run A-B (Revised)",
  observation: "Updated observation - rerouted section C.",
  color: "newColorIdValue", // Example of updating an optional field
};

sdk.duct.updateById('ductId', updateDuctData).then(() => {
  console.log('Duct updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching Ducts

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.duct.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('Ducts:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "ductIdABC",
      "name": "Main Duct Run A-B (Revised)",
      "project": "projectId123",
      "ductType": "ductTypeIdXYZ",
      "edgeA": "junctionBoxIdA",
      "edgeB": "junctionBoxIdB",
      "points": ["pointId1", "pointId2", "pointId3"],
      "tags": ["core-network", "phase1", "revised"],
      "implanted": true,
      "observation": "Updated observation - rerouted section C.",
      "color": "newColorIdValue",
      "shared": false,
      "length": 155.20,
      "immediateParent": null,
      "parent": null,
      "index": 1,
      "typeColor": { "regular": "#FF5733", "notImplanted": "#FFC300" },
      "external_id": null,
      "createdAt": "2023-10-30T10:00:00.000Z",
      "updatedAt": "2023-10-30T10:15:00.000Z", // Assuming updated
      "id": "ductIdABC"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a Duct by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.duct.findById('ductId').then((duct) => {
  console.log('Duct:', duct);
});
```
Response example:
```json
{
  "_id": "ductIdABC",
  "name": "Main Duct Run A-B (Revised)",
  "project": "projectId123",
  "ductType": "ductTypeIdXYZ",
  "edgeA": "junctionBoxIdA",
  "edgeB": "junctionBoxIdB",
  "points": ["pointId1", "pointId2", "pointId3"],
  "tags": ["core-network", "phase1", "revised"],
  "implanted": true,
  "observation": "Updated observation - rerouted section C.",
  "color": "newColorIdValue",
  "shared": false,
  "length": 155.20,
  "immediateParent": null,
  "parent": null,
  "index": 1,
  "typeColor": { "regular": "#FF5733", "notImplanted": "#FFC300" },
  "external_id": "ext-duct-789",
  "createdAt": "2023-10-30T10:00:00.000Z",
  "updatedAt": "2023-10-30T10:15:00.000Z",
  "id": "ductIdABC"
}
```

### Deleting a Duct

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.duct.deleteById('ductId').then(() => {
  console.log('Duct deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```