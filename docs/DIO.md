# DIO Module

This document provides a concise guide to the DIO module, focusing on the DIO model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### DIO

Defines the structure for DIOs.

```typescript
type DIO = {
  id: string;
  kind: "DIO";
  connectables: {
    input: (string | null)[];
    output: (string | null)[];
  };
  dioType: string | DIOType;
  observation?: string;
  name: string;
  project: string; // Added
  tray_number: number;
  port_labels: string[];
  tray_labels: string[];
  input_label: string[];
  output_label: string[];
  attenuation?: number; // Added
  isDrop?: boolean; // Added
  external_id?: any;
  shelf?: string | NetworkConnector; // NetworkConnector not defined in MD snippet
};
```

### CreateDIODTO

Defines the structure for creating a DIO.

```typescript
type CreateDIODTO = {
  dioType: string;
  project: string; // Added: Required
  parent: string; // Added: Required (ID of Pop, Shelf, etc.)
  name?: string; // Changed to optional
  observation?: string;
  attenuation?: number; // Added: Optional
  tags?: string[]; // Added: Optional
  external_id?: any;
};
```

### UpdateDIODTO

Defines the structure for updating a DIO.

```typescript
type UpdateDIODTO = {
  dioType?: string;
  observation?: string;
  name?: string;
  tray_number?: number;
  port_labels?: string[];
  tray_labels?: string[];
  input_label?: string[];
  output_label?: string[];
  connectables?: { // Added: Optional
    input?: (string | null)[];
    output?: (string | null)[];
  };
  attenuation?: number; // Added: Optional
  isDrop?: boolean; // Added: Optional
  external_id?: any;
  shelf?: string;
};
```

## Example Usage

### Creating a DIO

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateDIODTO } from './DIO'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newDIOData = { // CreateDIODTO type assumed to be available
  dioType: "dioTypeIdValue",
  project: "projectIdValue", // Added required field
  parent: "popIdValue", // Added required field (e.g., ID of a POP or Shelf)
  name: "DIO-SiteA-01",
  observation: "Main distribution frame for Site A",
  // attenuation, tags, external_id are optional
};

sdk.dio.create(newDIOData).then((dio) => {
  console.log('DIO created:', dio);
});
```
Response example:
```json
{
  "_id": "dioIdXYZ",
  "dioType": "dioTypeIdValue",
  "project": "projectIdValue",
  "parent": "popIdValue",
  "name": "DIO-SiteA-01",
  "observation": "Main distribution frame for Site A",
  "kind": "DIO",
  "connectables": { "input": [], "output": [] }, // Default or based on DIOType
  "tray_number": 0, // Default or based on DIOType
  "port_labels": [], // Default or based on DIOType
  "tray_labels": [], // Default or based on DIOType
  "input_label": [], // Default or based on DIOType
  "output_label": [], // Default or based on DIOType
  "attenuation": null,
  "isDrop": false, // Default from NetworkConnectable
  "tags": [],
  "external_id": null,
  "shelf": null,
  "createdAt": "2023-10-29T12:00:00.000Z",
  "updatedAt": "2023-10-29T12:00:00.000Z",
  "id": "dioIdXYZ"
}
```

### Updating a DIO

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateDIODTO } from './DIO'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateDIOData = { // UpdateDIODTO type assumed to be available
  observation: "Updated observation for DIO-SiteA-01",
  name: "DIO-SiteA-01 (Revised)",
  // Other fields like dioType, tray_number, labels, connectables, etc., are optional
};

sdk.dio.updateById('dioId', updateDIOData).then(() => {
  console.log('DIO updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching DIOs

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.dio.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('DIOs:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "dioIdXYZ",
      "dioType": "dioTypeIdValue",
      "project": "projectIdValue",
      "parent": "popIdValue",
      "name": "DIO-SiteA-01 (Revised)",
      "observation": "Updated observation for DIO-SiteA-01",
      "kind": "DIO",
      "connectables": { "input": ["someFiberId1"], "output": ["someFiberId2"] }, // Example
      "tray_number": 2, // Example
      "port_labels": ["P1", "P2"], // Example
      "tray_labels": ["Tray A", "Tray B"], // Example
      "input_label": ["IN-A"], // Example
      "output_label": ["OUT-A"], // Example
      "attenuation": 0.1, // Example
      "isDrop": false,
      "tags": ["critical"],
      "external_id": "ext-dio-001",
      "shelf": "shelfIdValue", // Example
      "createdAt": "2023-10-29T12:00:00.000Z",
      "updatedAt": "2023-10-29T12:05:00.000Z",
      "id": "dioIdXYZ"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a DIO by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.dio.findById('dioId').then((dio) => {
  console.log('DIO:', dio);
});
```
Response example:
```json
{
  "_id": "dioIdXYZ",
  "dioType": "dioTypeIdValue",
  "project": "projectIdValue",
  "parent": "popIdValue",
  "name": "DIO-SiteA-01 (Revised)",
  "observation": "Updated observation for DIO-SiteA-01",
  "kind": "DIO",
  "connectables": { "input": ["someFiberId1"], "output": ["someFiberId2"] },
  "tray_number": 2,
  "port_labels": ["P1", "P2"],
  "tray_labels": ["Tray A", "Tray B"],
  "input_label": ["IN-A"],
  "output_label": ["OUT-A"],
  "attenuation": 0.1,
  "isDrop": false,
  "tags": ["critical", "needs-review"],
  "external_id": "ext-dio-001",
  "shelf": "shelfIdValue",
  "createdAt": "2023-10-29T12:00:00.000Z",
  "updatedAt": "2023-10-29T12:05:00.000Z",
  "id": "dioIdXYZ"
}
```

### Deleting a DIO

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.dio.deleteById('dioId').then(() => {
  console.log('DIO deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```

