# Password Validation Form

> Technical challenge built for a job application process. Shared here as a code sample.

A React + TypeScript form that validates a numeric password against a set of business rules in real time, shows every broken rule at once, and submits the result to the challenge's API.

## The challenge

Build a form with **name**, **email** and **password** fields. The password is valid only if it follows all of these rules:

- It has exactly **6 digits**
- Its value is **between 184759 and 856920**
- It contains **at least one pair of equal adjacent digits** (e.g. `22` in `122345`)
- Its digits **never decrease** from left to right (e.g. `111123` or `135679`)

When the password is valid, the form sends the data to an API endpoint provided by the challenge.

For example, `234556` is valid, while `234554` fails because the last digit decreases.

## What was delivered

- Form built with **React Hook Form** and **Zod**, validating name and email as the user types
- Password rules implemented as a Zod schema with `superRefine`, returning **all failing rules at once** instead of only the first one
- Show/hide password toggle and a responsive layout for mobile and desktop
- Submit button enabled only when the form is valid, with success and error feedback after sending
- **Unit and component tests** with Jest and React Testing Library

## Tech stack

React 18 · TypeScript · Vite · Material UI · React Hook Form · Zod · Axios · Jest · React Testing Library

## Getting started

```bash
yarn
yarn dev
```

### Running the tests

```bash
yarn test
```

The suite checks that the form renders correctly and that each password rule returns the expected error messages.

## Project structure

- **`src/pages/Password`** — The form component and the Zod schema for name and email
- **`src/utils/validatePassword.ts`** — The password rules, isolated from the UI so they can be tested on their own
- **`src/services`** — Axios instance and a small `post` wrapper that normalizes success and error responses
- **`src/pages/Tests`** — Jest and Testing Library tests

## Design decisions

- **Password rules outside the form schema:** React Hook Form surfaces one error per field, but the challenge called for showing every broken rule at the same time. Keeping the rules in `validatePassword` and running them on submit made it possible to list all of them, and also made the rules easy to test without rendering the UI.
- **Zod for both the form and the rules:** a single validation library for everything, with typed inputs and outputs inferred from the schema.

## With more time, I would add

- A test for the happy path (a valid password) and for the submit flow with a mocked API
- The API URL in an environment variable instead of hardcoded
- Stricter typing in the form and service layer, replacing the remaining `any`s
