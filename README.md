# OZmap SDK

OZmap is a solution by devOZ. Based in Florianópolis since 2012, we develop software focused on facilitating the mapping of georeferenced data with the intention of generating intelligent information for strategic decisions.

## What is OZmap SDK?

The OZmap SDK is a tool designed to help developers interact with the OZmap API, providing a streamlined interface for managing georeferenced data. This SDK includes various methods for creating, updating, retrieving, and deleting different models within the OZmap ecosystem, such as projects, cables, boxes, poles, and more.

## Features

- **CRUD Operations**: Easily create, read, update, and delete data.
- **Data Mapping**: Simplifies the interaction with georeferenced data.
- **Batch Operations**: Perform batch updates and retrieves efficiently.
- **Pagination Support**: Handle large datasets with pagination.
- **Filter and Query**: Advanced filtering and querying capabilities.

## Installation

To install the OZmap SDK, use npm:

```bash
npm i --save @ozmap/ozmap-sdk
```

## Usage

### Using login and password

```typescript
import OZMapSDK from '@ozmap/ozmap-sdk';

const sdk = new OZMapSDK('https://api.example.com', { login: 'your-ozmap-login', password: 'your-ozmap-password' });
```

### Using API Key

```typescript
import OZMapSDK from '@ozmap/ozmap-sdk';

const sdk = new OZMapSDK('https://api.example.com', { apiKey: 'your-ozmap-api-key' });
```

## CRUD operations

### Create

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newPopData = { // CreatePopDTO definition assumed to be available
  name: "New Pop",
  hierarchyLevel: 1,
  popType: "popTypeId",
  pole: "poleId",
  implanted: true,
};

sdk.pop.create(newPopData).then((pop) => {
  console.log('Pop created:', pop);
});
```

### Update

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updatePopData = { // UpdatePopDTO definition assumed to be available
  name: "Updated Pop",
  hierarchyLevel: 2,
};

sdk.pop.updateById('popId', updatePopData).then(() => {
  console.log('Pop updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetch

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.pop.find({ page: 1, limit: 10, filter: [
    {
      property: "name",
      operator: FilterOperator.EQUAL,
      value: "Popname",
    }]
}).then((pagination) => {
  console.log('Pops:', pagination);
});
```

### Fetch by id

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.pop.findById('popId').then((pop) => {
  console.log('Pop:', pop);
});
```

### Delete

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.pop.deleteById('popId').then(() => {
  console.log('Pop deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```

## API instance methods

For making non-CRUD operations, such as viability or any other that isn't included in an element route, you can use the `apiInstance` of the SDK.

### Get

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.apiInstance.get<OUTPUT>({
    route: 'ftth-viability/radius',
    options: { params: { lat, lng } },
}).then((response) => {
    console.log('Response:', response);
});
```


### Post

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.apiInstance.post<INPUT, OUTPUT>({
  route: 'custom/route',
  inputData: { key: 'value' },
  options: { headers: { 'Custom-Header': 'value' } },
}).then((response) => {
  console.log('Response:', response);
});
```

### Patch

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.apiInstance.patch<INPUT>({
    route: 'custom/route',
    inputData: { key: 'newValue' },
    options: { headers: { 'Custom-Header': 'value' } },
}).then(() => {
    console.log('Data updated');
});
```

### Delete

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.apiInstance.delete({
    route: 'custom/route',
    options: { headers: { 'Custom-Header': 'value' } },
}).then(() => {
    console.log('Data deleted');
});
```


## Documentation

## Models

### Boxes

- [Base Box](./docs/BASEBOX.md)
- [Box](./docs/BOX.md)
- [Box Template](./docs/BOXTEMPLATE.md)
- [Box Type](./docs/BOXTYPE.md)

### Building

- [Building](./docs/BUILDING.md)
- [Building Type](./docs/BUILDINGTYPE.md)

### Cables

- [Cable](./docs/CABLE.md)
- [Cable Stub](./docs/CABLESTUB.md)
- [Cable Type](./docs/CABLETYPE.md)

### Clients

- [FTTH Client](./docs/FTTHCLIENT.md)

### Colors

- [Color](./docs/COLOR.md)

### Connectors

- [Connector](./docs/CONNECTOR.md)
- [Connector Type](./docs/CONNECTORTYPE.md)
- [Network Connectable](./docs/NETWORKCONNECTABLE.md)
- [Network Connector](./docs/NETWORKCONNECTOR.md)

### Cords

- [Cord](./docs/CORD.md)

### Devices

- [DIO](./docs/DIO.md)
- [DIO Type](./docs/DIOTYPE.md)

### Ducts

- [Duct](./docs/DUCT.md)
- [Duct Type](./docs/DUCTTYPE.md)

### Fibers

- [Fiber](./docs/FIBER.md)
- [Fiber Profile](./docs/FIBERPROFILE.md)

### Files

- [File](./docs/FILE.md)

### Fusion

- [Fusion](./docs/FUSION.md)
- [Fusion Type](./docs/FUSIONTYPE.md)

### Horizontal Condominium

- [Horizontal Condominium](./docs/HORIZONTALCONDOMINIUM.md)

### Junction Boxes

- [Junction Box](./docs/JUNCTIONBOX.md)
- [Junction Box Type](./docs/JUNCTIONBOXTYPE.md)

### OLT

- [OLT](./docs/OLT.md)
- [OLT Type](./docs/OLTTYPE.md)

### Passing

- [Passing](./docs/PASSING.md)

### Pendencies

- [Pendency](./docs/PENDENCY.md)
- [Pendency Type](./docs/PENDENCYTYPE.md)

### Points

- [Base Point](./docs/BASEPOINT.md)
- [Point](./docs/POINT.md)


### Poles
- [Pole](./docs/POLE.md)
- [Pole Type](./docs/POLETYPE.md)

### PON

- [PON](./docs/PON.md)

### POP
- [POP](./docs/POP.md)
- [POP Type](./docs/POPTYPE.md)

### POST
- [Post](./docs/POST.md)

### Projects

- [Project](./docs/PROJECT.md)
- [Project Group](./docs/PROJECTGROUP.md)

### Properties

- [Property](./docs/PROPERTY.md)
- [Prospect](./docs/PROSPECT.md)

### Regions

- [Region](./docs/REGION.md)
- [Region Type](./docs/REGIONTYPE.md)

### Roles

- [Role](./docs/ROLE.md)

### Shelves

- [Shelf](./docs/SHELF.md)
- [Shelf Type](./docs/SHELFTYPE.md)

### Slots

- [Slot](./docs/SLOT.md)

### Splitters

- [Splitter](./docs/SPLITTER.md)
- [Splitter Type](./docs/SPLITTERTYPE.md)

### Switches

- [Switch](./docs/SWITCH.md)
- [Switch Type](./docs/SWITCHTYPE.md)

### System

- [System Configuration](./docs/SYSTEMCONFIG.md)
- [Tags](./docs/TAG.md)
- [Users](./docs/USER.md)

### Vertical Condominium
- [Vertical Condominium](./docs/VERTICALCONDOMINIUM.md)
- [Vertical Condominium Unit](./docs/VERTICALCONDOMINIUMUNIT.md)

### Warehouse
- [Warehouse](./docs/WAREHOUSE.md)
- [Warehouse Item](./docs/WAREHOUSEITEM.md)
- [Warehouse Item Type](./docs/WAREHOUSEITEMTYPE.md)


## Documentation Contribution Guide
Welcome contributors! To maintain consistency and quality in our documentation, please follow these guidelines when adding or updating documentation for models:

**Structure of Model Documentation:**

Each model should have its own Markdown file in the `/docs` directory (e.g., `docs/MYMODEL.md`). The file should generally follow this structure:

1.  **Model Name Heading:** (e.g., `# MyModel Module`)
2.  **Brief Description:** A short explanation of what the model represents and its purpose.
3.  **Model Definition:** The TypeScript type definition for the model.
4.  **DTO Definitions:** TypeScript type definitions for `CreateMyModelDTO` and `UpdateMyModelDTO` (if applicable).
5.  **Example Usage Heading:** (e.g., `## Example Usage`)
6.  **CRUD Operations:**
    *   For each standard operation (Create, Find (List), FindById, Update, Delete):
        *   A subheading (e.g., `### Creating a MyModel`).
        *   A code snippet in TypeScript showing how to use the SDK method.
        *   An example JSON response for the operation. If an operation returns no content (e.g., `updateById`, `deleteById` often return `Promise<void>`), note this and optionally provide guidance on how to verify the operation's success (e.g., by attempting to fetch the resource afterwards or by confirming the promise resolves without error). Ensure all placeholders like `ozmapURL` and `yourApiKey` are clearly indicated.

**Key Guidelines:**

*   **Clarity:** Write clear and concise descriptions.
*   **Completeness:** Ensure all CRUD operations are documented with code examples and their respective JSON responses.
*   **Accuracy:** Keep documentation synchronized with any changes in the SDK's models, DTOs, or methods.
*   **Consistency:** Follow the style and formatting of existing documentation files. Refer to other files in the `docs/` directory as a template.

Your contributions to improving and expanding the documentation are highly appreciated!

## API

For detailed information about the API endpoints and how to use them, please refer to the [OZmap API Documentation](https://ozmap.stoplight.io/docs/ozmap/f20b389eedb19-o-zmap).

## License

This project is licensed under the MIT License.

## Links

- [OZmap Website](https://ozmap.net/)
- [OZmap API Documentation](https://ozmap.stoplight.io/docs/ozmap/f20b389eedb19-o-zmap)