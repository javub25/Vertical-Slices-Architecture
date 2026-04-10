# Vertical-Slices-Architecture
Clean Frontend Archuitecture - Vertical Slices


## 📗 📂 Domain Layer

Contains business rules that the application must follow.

### 📂 models/

Defines how data looks like such as **TypeScript (interfaces, types) or JavaScript classes**.

FileName: **domain/models/product.models.ts**


```ts

export type ProductId = string;

export interface Product {
  id: ProductId;     
  name: string;
  description: string;
  price: number;       
}
```

### 📂 rules/

Contains functions related to the domain models.

FileName: **domain/rules/product.rules.ts**

```ts
export const isPriceValid = (product: Product): boolean => {
  return product.price > 0;
};
```