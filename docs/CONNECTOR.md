# Connector Module

This document provides a detailed guide to the Connector module, focusing on the Connector model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### Connector

Defines the structure for connectors.

```typescript
type Connector = {
  _id: string;
  id: string;
  kind: 'Connector'; // Simplified from NetworkConnectorKind.CONNECTOR
  name?: string;
  parent: string; // ID of the parent entity (e.g., Box, DIO)
  project: string; // ID of the project
  connectorType: string; // ID of the ConnectorType
  connectables: (string | null)[]; // Array of IDs of connected entities or null
  isDrop?: boolean;
  attenuation?: number;
  tags?: string[];
  createdAt: string | Date;
  updatedAt: string | Date;
  // Additional properties from NetworkConnectorSchema might be relevant depending on usage
};
```

### CreateConnectorDTO

Defines the structure for creating a connector.

```typescript
type CreateConnectorDTO = {
  parent: string; // ID of the parent entity (e.g., Box, DIO)
  connectorType: string; // ID of the ConnectorType
  name?: string;
  attenuation?: number;
  tags?: string[];
  external_id?: any;
};
```

### UpdateConnectorDTO

Defines the structure for updating a connector.

```typescript
type UpdateConnectorDTO = {
  parent?: string; // ID of the parent entity (e.g., Box, DIO)
  connectorType?: string; // ID of the ConnectorType
  name?: string;
  attenuation?: number;
  tags?: string[];
  external_id?: any;
};
```

## Example Usage

### Create a Connector

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateConnectorDTO } from './Connector'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newConnectorData = { // CreateConnectorDTO type assumed to be available
  parent: 'parentId123', // e.g., ID of a Box or DIO
  connectorType: 'connectorTypeIdABC',
  name: 'CON-001',
  // attenuation, tags, external_id are optional
};

sdk.connector.create(newConnectorData).then((connector) => {
  console.log('Connector created:', connector);
});
```
Response example:
```json
{
  "_id": "connectorIdXYZ",
  "parent": "parentId123",
  "connectorType": "connectorTypeIdABC",
  "name": "CON-001",
  "kind": "Connector",
  "project": "projectIdAssociatedWithParent",
  "connectables": [null, null], // Example for a 2-position connector
  "isDrop": false,
  "attenuation": 0.25, // Example default or calculated value
  "tags": [],
  "createdAt": "2023-10-28T16:00:00.000Z",
  "updatedAt": "2023-10-28T16:00:00.000Z",
  "id": "connectorIdXYZ"
}
```

### Update a Connector

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateConnectorDTO } from './Connector'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateConnectorData = { // UpdateConnectorDTO type assumed to be available
  connectorType: 'updatedConnectorTypeId',
  name: "CON-001-Renamed"
};

sdk.connector.updateById('connectorId', updateConnectorData).then(() => {
  console.log('Connector updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```
### Fetching Connectors

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.connector.find({ page: 1, limit: 10 }).then((pagination) => { // Corrected to sdk.connector
  console.log('Connector:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "connectorIdXYZ",
      "parent": "parentId123",
      "connectorType": "connectorTypeIdABC",
      "name": "CON-001",
      "kind": "Connector",
      "project": "projectIdAssociatedWithParent",
      "connectables": [null, "someConnectableId"],
      "isDrop": false,
      "attenuation": 0.25,
      "tags": ["tag1"],
      "createdAt": "2023-10-28T16:00:00.000Z",
      "updatedAt": "2023-10-28T16:05:00.000Z",
      "id": "connectorIdXYZ"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a Connector by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.connector.findById('connectorIdXYZ').then((connector) => { // Corrected to sdk.connector and variable name
  console.log('Connector:', connector);
});
```
Response example:
```json
{
  "_id": "connectorIdXYZ",
  "parent": "parentId123",
  "connectorType": "connectorTypeIdABC",
  "name": "CON-001",
  "kind": "Connector",
  "project": "projectIdAssociatedWithParent",
  "connectables": [null, "someConnectableId"],
  "isDrop": false,
  "attenuation": 0.25,
  "tags": ["tag1", "important"],
  "createdAt": "2023-10-28T16:00:00.000Z",
  "updatedAt": "2023-10-28T16:05:00.000Z",
  "id": "connectorIdXYZ"
}
```

### Deleting a Connector

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.connector.deleteById('connectorIdXYZ').then(() => { // Corrected to sdk.connector
  console.log('Connector deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```