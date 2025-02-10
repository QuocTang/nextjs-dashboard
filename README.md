## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

## setup and interact with database pg

There are a few cases where you have to write database queries:

- When creating your API endpoints, you need to write logic to interact with your database.
- If you are using React Server Components (fetching data on the server), you can skip the API layer, and query your database directly without risking exposing your database secrets to the client.

## Server Components

- Server Components support JavaScript Promises, providing a solution for asynchronous tasks like data fetching natively. You can use async/await syntax without needing useEffect, useState or other data fetching libraries.
- Server Components run on the server, so you can keep expensive data fetches and logic on the server, only sending the result to the client.
- Since Server Components run on the server, you can query the database directly without an additional API layer. This saves you from writing and maintaining additional code.

### The page is an async server component

```tsx
// pages/index.tsx
import { fetchCardData } from "../lib/data";

export default async function Home() {
  const data = await fetchCardData();
  return (
    <div>
      <h1>Home Page</h1>
      <p>{data}</p>
    </div>
  );
}
```

## Static Redering

- With static rendering, data fetching and rendering happens on the server at build time (when you deploy) or when revalidating data. (Faster Websites - Reduced Server Load - SEO)
- Static rendering is useful for UI with no data or data that is shared across users, such as a static blog post or a product page. It might not be a good fit for a dashboard that has personalized data which is regularly updated.

## Route Groups

- In the app directory, nested folders are normally mapped to URL paths. However, you can mark a folder as a Route Group to prevent the folder from being included in the route's URL path.
- A route group can be created by wrapping a folder's name in parenthesis: (folderName)

## Suppense

- Suppense is a feature that allows you to display a loading state while waiting for data to load. It provides a better user experience by showing a loading indicator while the data is being fetched.

## Hooks

1. useDeferredValue

- useDeferredValue is integrated with <Suspense>. If the background update caused by a new value suspends the UI, the user will not see the fallback. They will see the old deferred value until the data loads.
- When an update is inside a Transition, useDeferredValue always returns the new value and does not spawn a deferred render, since the update is already deferred.
  Mục đích: Tối ưu hóa hiệu suất render bằng cách trì hoãn cập nhật các giá trị không ưu tiên, giúp giao diện người dùng phản hồi nhanh hơn.
  REACT.DEV

Cách hoạt động: Trả về một phiên bản "trì hoãn" của giá trị đầu vào; React sẽ ưu tiên các tác vụ quan trọng trước khi cập nhật giá trị này.
REACT.DEV

Khi sử dụng: Hữu ích khi xử lý các tác vụ tốn kém tài nguyên, như lọc danh sách lớn dựa trên đầu vào người dùng, để duy trì tính phản hồi của giao diện.
JOSHWCOMEAU.COM

Lưu ý: Không thay thế cho các kỹ thuật tối ưu hóa khác như debouncing hay throttling, nhưng cung cấp một cách tiếp cận bổ sung để quản lý hiệu suất trong React.
