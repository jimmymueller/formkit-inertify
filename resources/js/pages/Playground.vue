<template>
  <FormKit
    type="form"
    submit-label="Login"
    @submit="(fields, node) => node.context?.inertia.post(
      '/login',
      fields,
      // Form backend validation does not display for each field if ANY options param is set, even an empty {}
      // {}
      {
        onBefore: (visit, node) => {
          $console.log(visit, node);
          // Also it would be helpful to be able to return false from onBefore to cancel the request per the inertia docs
          // https://inertiajs.com/manual-visits#event-callbacks
        },
        onError: (errors, node) => {
          $console.log(errors);
          node.setErrors('testError', 'this should work too?'); //is this node being passed through correctly?
        }
      }
    )">
    <!-- <FormKit type="text" label="E-mail" name="email" validation="required|email" />
    <FormKit type="password" label="Password" name="password" validation="required" autocomplete /> -->
    <FormKit type="text" label="E-mail" name="email" />
    <FormKit type="password" label="Password" name="password" autocomplete />
  </FormKit>

  <pre>{{ $attrs }}</pre>
</template>
