Here's a Bootstrap-styled message you can use to request users to sign up or log in to access a timer feature:

```html
<div class="alert alert-warning alert-dismissible fade show" role="alert">
    <strong>Access Restricted!</strong> To use the timer feature, please <a href="/signup" class="alert-link">sign up</a> or <a href="/login" class="alert-link">log in</a> to your account.
    <button type="button" class="close" data-dismiss="alert" aria-label="Close">
        <span aria-hidden="true">&times;</span>
    </button>
</div>
```

This message uses Bootstrap's alert component to create a visually appealing notification that encourages users to either sign up or log in. You can customize the links to point to your actual signup and login pages.