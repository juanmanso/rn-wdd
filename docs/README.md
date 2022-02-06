# Why bother?

### Based on the article [Widget Driven Development](https://dev.to/aantipov/widget-driven-development-1n5m) by [Alexey Antipov](https://dev.to/aantipov)

Motivated by some problems that regularly appear on React Native applications (and are generally handled with a very use case-specific solution), but also by the goal of making development and features more [orthogonal](https://www.freecodecamp.org/news/orthogonality-in-software-engineering/), a new change of scope must be made.

# Standardized vs Proposed design

<details>
<summary>Click to expand/contract design notes</summary>

## Standardized design

<details>
  <summary>Click to expand/contract detail</summary>

Generally, components are developed as a wrapper container that contains representational components (dummy UI layers) and its inner logic. This approach is great because it enables re-usability without code duplication.

| <image alt='Schematic of our current components structural design' src='https://res.cloudinary.com/practicaldev/image/fetch/s--gmOxeBWT--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kbbvb9ncnr6bvhcozu5i.png' width=500> |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |

_Schematic of regular component's structural design_

However, to **avoid redundant requests** for information that was already requested, external data is either drilled down (parent prop drilling) or shared using several levels of state (React Context, Redux). This generates a **big coupling** between views/components/state managers, along with the **logic overhead** to handle and/or validate the information.

|                                                                                                                  _Prop drilling by parent approach_                                                                                                                   |                                                                                                                   _Shared state_                                                                                                                   |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| <image alt='Prop drilling by parent approach' src='https://res.cloudinary.com/practicaldev/image/fetch/s--ycFa3c8r--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/efp3s243lqvo1xyykyy2.png' width=500> | <image alt='Shared state' src='https://res.cloudinary.com/practicaldev/image/fetch/s--rWjmuJfg--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xcimiwli8pey0xk4c6gw.png ' width=500> |

</details>

## Proposed design

<details>
  <summary>Click to expand/contract detail</summary>

To thrive on orthogonality (total decoupling of components), keeping them simple to maintain and self-contained to be easily tested, the **Widget Driven Development** is proposed.

| <image alt='Schematic of widgets requesting for their data' src='https://res.cloudinary.com/practicaldev/image/fetch/s--cKhUdzDU--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kyhk7wq6t9vw6t72zp7n.png' width=500> |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |

_Schematic of widgets asking for their data themselves_

By adding an API wrapper on the frontend side, we can **let the widgets do all their requests internally** since it won't overload the original backend (but let them think they are doing that).

Additionally, this API wrapper can **efficiently handle request**, providing the widgets:

- The same version of the external data
- Validation of received information

Finally, with this approach we can keep let widgets be the owner of their actions by asking for the required information **minimizing uncontrolled side-effects**.

<details>
  <summary>Click to see an example</summary>

> _It's easy to see that some information is shared across stacks, views and components such as **user information** or **wallet information**. Some part of the app might alter that information for internal use, but it might provoke a change that would affect some other functionality. Thus, decreasing coupling of information is a key element of the design to decrease side effects._

</details>

</details>

</details>

## Possible implementation

Instead of developing the API Wrapper layer, we shall use a well maintained package such as `react-query`. The library is literally a wrapper to do requests (using `fetch`, `axios`, etc.) to access their responses through the provided React Hooks.

The way to implement the "data logic" part of the widget, would be to create custom hooks that handle the proper logic but use the `react-query` hooks to get the necessary information. Then, processed external and internal data is passed along through the custom hook, leaving the rest of the widget to be fully representational.

### Setup

- Incorporate `react-query` dependency
- Setup `QueryClient` and provider

### Development

**Base guidelines**:

- Add requests to `react-query` requests by creating a hook on `queries` folder
- Develop feature using the philosophy:
  - `CustomHook = Query + InnerLogic`
  - `Widget = CustomHook + RepresentationalComponents`
