# Vertical-Slices-Architecture
Clean Frontend Archuitecture - Vertical Slices


## 📗 📂 Domain Layer

Contains business rules that the application must follow.  
Those rules won't changed across application.  
**No React, Angular or database code allowed.**

```css
src/
└── features/
    ├── products/
         ├── domain/
           ├── models/
           |  └── Product.models.ts
           ├── constants/
           |  └── Product.constants.ts
           ├── rules/
              └── Product.rules.ts
          ├── presentation/
               ├── ui
                   └── Product.ui.tsx   
```
Architecture with products feature.  

### 📂 models/

Defines data shape names such as:
  - TypeScript **(interfaces, types)**.
  - JavaScript **classes with their own methods**.

```ts
export type ProductId = string;

export interface Product {
  id: ProductId;     
  name: string;
  description: string;
  price: number;   
}
```

### 📂 constants

We want to specify price product configuration allowed in our application.   
constants folder holds it in one place.

```ts

export const PRODUCT_PRICE = {
  MIN_PRICE: 0,
  ERROR_CODE: 'INVALID_PRICE',
  ERROR_MESSAGE: 'Product price must be zero or greater',
} as const;
```


### 📂 rules/

Contains actions to validate how a Product should be.

Example, ensure a product has a valid price.

```ts
export const isPriceValid = (price: number): boolean => {
  return price >= PRODUCT_PRICE.MIN_PRICE;
}

export const ensurePriceIsValid = (product: Product): ValidationResult => {
  const isValid = isPriceValid(product.price);

   if(isValid)
   {
     return { isValid: true, errors: [] };
   }

   return {
      isValid: false,
      errors: [PRODUCT_PRICE]
  }
};
```



 ## 📂 🖥️  Presentation

 Only knows **what to show in the UI**.
 
 ✅ Statements to define what to show in the UI.   
 ✅ Components, hooks, routing, state.  


```ts
export default function UserDashboardPage() {
  const { metrics, isLoading, error } = useDashboardData(userId);

  if (isLoading)
     return <DashboardSkeleton />;
  if (error)
     return <ErrorBanner error={error} />;

  return (
    <PageLayout title="Dashboard">
      <MetricGrid metrics={metrics} />
    </PageLayout>
  );
}
```

### 📂 ui

Views only used for UserDashboardPage view.

```ts
features/dashboard/
 └── presentation/
      ├── UserDashboardPage.tsx 
      └── ui/                   
           ├── MetricCard.tsx
           ├── DashboardHeader.tsx
      └── hooks/                   
           ├── useDashboardData.ts
```


 ### 📜 Rules
- **Presentation**: If it needs to **display data or capture user input** **(UI, framework-hooks, DOM events)**.
- **Infraestructure**: If it **talks to anything outside** the app **(databases, APIs, LocalStorage)**.
- **Domain**: If it defines **what the data is and how business works** **(Shapes, math, logic)**.
- **Application**: If it coordinates the steps of a specific task.

<img width="700" height="800" alt="architecture" src="https://github.com/user-attachments/assets/f204fee4-f94c-4f31-aab4-d45425ff05c8" />


