# Next.js 15 App Directory Fetch Memory Leak

This repository demonstrates a potential memory leak in Next.js 15's `app` directory when using the `fetch` API within a component's `useEffect` hook.  The problem arises when the component unmounts before the asynchronous `fetch` operation completes.

## Problem
The `fetch` call continues even after the component is unmounted, potentially leading to memory leaks and unexpected behavior because there's no component left to handle the resolved data.  Standard cleanup in `useEffect`'s return function doesn't address this because the `fetch` operation happens outside of the component's lifecycle control.

## Solution
The solution involves using the AbortController API to cancel the fetch request when the component unmounts. This prevents unnecessary requests and resource consumption.