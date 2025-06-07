# ConnectorType Module

This document provides a concise guide to the ConnectorType module, focusing on the ConnectorType model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### ConnectorType

Defines the structure for connector types.

```typescript
type ConnectorType = {
  id: string;
  code: string;
  brand?: string;
  mold?: string;
  description?: string;
  loss: number;
  isDrop: boolean;
  external_id?: any;
};
```

### CreateConnectorTypeDTO

Defines the structure for creating a connector type.

```typescript
type CreateConnectorTypeDTO = {
  code: string;
  brand?: string;
  mold?: string;
  description?: string;
  loss: number;
  isDrop: boolean;
  external_id?: any;
};
```

### UpdateConnectorTypeDTO

Defines the structure for updating a connector type.

```typescript
type UpdateConnectorTypeDTO = {
  code?: string;
  brand?: string;
  mold?: string;
  description?: string;
  loss?: number;
  isDrop?: boolean;
  external_id?: any;
};
```

## Example Usage

### Creating a ConnectorType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateConnectorTypeDTO } from './ConnectorType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newConnectorTypeData = { // CreateConnectorTypeDTO type assumed to be available
  code: "SC/APC",
  loss: 0.3,
  isDrop: false,
  brand: "Generic",
  mold: "SC",
  description: "Standard SC/APC Connector",
  // external_id is optional
};

sdk.connectorType.create(newConnectorTypeData).then((connectorType) => {
  console.log('ConnectorType created:', connectorType);
});
```
Response example:
```json
{
  "_id": "connectorTypeId123",
  "code": "SC/APC",
  "loss": 0.3,
  "isDrop": false,
  "brand": "Generic",
  "mold": "SC",
  "description": "Standard SC/APC Connector",
  "external_id": null,
  "createdAt": "2023-10-28T17:00:00.000Z",
  "updatedAt": "2023-10-28T17:00:00.000Z",
  "id": "connectorTypeId123"
}
```

### Updating a ConnectorType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateConnectorTypeDTO } from './ConnectorType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateConnectorTypeData = { // UpdateConnectorTypeDTO type assumed to be available
  description: "Updated SC/APC Connector description",
  loss: 0.25,
};

sdk.connectorType.updateById('connectorTypeId', updateConnectorTypeData).then(() => {
  console.log('ConnectorType updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching ConnectorTypes

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.connectorType.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('ConnectorTypes:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "connectorTypeId123",
      "code": "SC/APC",
      "loss": 0.3,
      "isDrop": false,
      "brand": "Generic",
      "mold": "SC",
      "description": "Standard SC/APC Connector",
      "external_id": null,
      "createdAt": "2023-10-28T17:00:00.000Z",
      "updatedAt": "2023-10-28T17:00:00.000Z",
      "id": "connectorTypeId123"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a ConnectorType by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.connectorType.findById('connectorTypeId').then((connectorType) => {
  console.log('ConnectorType:', connectorType);
});
```
Response example:
```json
{
  "_id": "connectorTypeId123",
  "code": "SC/APC",
  "loss": 0.3,
  "isDrop": false,
  "brand": "Generic",
  "mold": "SC",
  "description": "Standard SC/APC Connector",
  "external_id": "ext-scapc-001",
  "createdAt": "2023-10-28T17:00:00.000Z",
  "updatedAt": "2023-10-28T17:05:00.000Z",
  "id": "connectorTypeId123"
}
```

### Deleting a ConnectorType

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.connectorType.deleteById('connectorTypeId').then(() => {
  console.log('ConnectorType deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```
