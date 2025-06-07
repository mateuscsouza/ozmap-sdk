# BaseBox Module

BaseBox is a parent class. For more information, visit its children documentation.
Note: The BaseBox model is generally read-only through its specific endpoint. Create, Update, and Delete operations are typically performed on its derived models (like Box, Building, etc.).

- [Box](./BOX.md)<br>
- [Building](./BUILDING.md)<br>
- [Property](./PROPERTY.md)<br>
- [POP](./POP.md)<br>
- [CableStub](./CABLESTUB.md)<br>

## Models

### BaseBox

Defines the structure for base boxes.

```typescript
type BaseBox = {
  tags?: string[]; // default: []
  project: string;
  cables?: string[]; // default: []
  pole?: string;
  name?: string;
  kind: string; // Enum: 'Box', 'Building', 'Property', 'Pop'
  observation?: string;
  coords: [number, number];
};
```

## Example Usage
### Fetching BaseBoxes

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.baseBox.find().then((pagination) => {
  console.log('BaseBoxes:', pagination);
});
```
Response example
```json
{
  "total": 100,
  "count": 1,
  "rows": [
    {
      "_id": "baseBoxId123",
      "tags": ["tagA", "tagB"],
      "project": "projectId456",
      "cables": ["cableId1", "cableId2"],
      "pole": "poleId789",
      "name": "Generic Base Box 1",
      "kind": "Box",
      "observation": "Sample observation 1.",
      "coords": [-48.5000, -27.6000],
      "createdAt": "2023-01-01T12:00:00.000Z",
      "updatedAt": "2023-01-01T12:30:00.000Z",
      "id": "baseBoxId123"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a BaseBox by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.baseBox.findById('baseBoxId').then((baseBox) => {
  console.log('BaseBox:', baseBox);
});
```
Response example
```json
{
  "_id": "baseBoxId123",
  "tags": ["tagA", "tagB"],
  "project": "projectId456",
  "cables": ["cableId1", "cableId2"],
  "pole": "poleId789",
  "name": "Generic Base Box",
  "kind": "Box",
  "observation": "This is a sample observation.",
  "coords": [-48.5000, -27.6000],
  "createdAt": "2023-01-01T12:00:00.000Z",
  "updatedAt": "2023-01-01T12:30:00.000Z",
  "id": "baseBoxId123"
}
```