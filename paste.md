To convert your navigation bar into Bootstrap tabs, you need to ensure that the structure adheres to Bootstrap's tab component requirements. Below is the modified code that uses Bootstrap tabs correctly:

```html
<ul id="top_nav_bar" class="nav nav-tabs" role="tablist">
    <li class="nav-item">
        <button class="nav-link active" id="home-tab" data-bs-toggle="tab" data-bs-target="#home" aria-controls="home" aria-selected="true">
            <i class="fas fa-home" style="margin-right:8px;"></i>Home
        </button>
    </li>
    <li class="nav-item">
        <button class="nav-link" id="streams-tab" data-bs-toggle="tab" data-bs-target="#streams" aria-controls="streams" aria-selected="false">
            <i class="fas fa-video" style="margin-right:8px;"></i>Streams
        </button>
    </li>
    <li class="nav-item">
        <button class="nav-link" id="favorites-tab" data-bs-toggle="tab" data-bs-target="#favorites" aria-controls="favorites" aria-selected="false">
            <i class="fas fa-star" style="margin-right:8px;"></i>Favorite Streams
        </button>
    </li>
    <li class="nav-item">
        <button class="nav-link" id="leaderboard-tab" data-bs-toggle="tab" data-bs-target="#leaderboard" aria-controls="leaderboard" aria-selected="false">
            <i class="fas fa-trophy" style="margin-right:8px;"></i>LeaderBoard
        </button>
    </li>
    <li class="nav-item">
        <button class="nav-link" id="about-tab" data-bs-toggle="tab" data-bs-target="#about" aria-controls="about" aria-selected="false">
            <i class="fas fa-info-circle" style="margin-right:8px;"></i>About
        </button>
    </li>
    <li class="nav-item dropdown" id="login-profile">
        <!-- Dropdown content can be added here if needed -->
    </li>
</ul>

<div class="container" id="auth-buttons">
    <div class="row text-center">
        <div class="col-6">
            <button class="btn" id="login-btn">Login</button>
        </div>
        <div class="col-6">
            <button class="btn" id="signup-btn">SignUp</button>
        </div>
    </div>
</div>

<!-- Tab content -->
<div class="tab-content">
    <div class="tab-pane fade show active" id="home" role="tabpanel" aria-labelledby="home-tab">
        <!-- Home content goes here -->
    </div>
    <div class="tab-pane fade" id="streams" role="tabpanel" aria-labelledby="streams-tab">
        <!-- Streams content goes here -->
    </div>
    <div class="tab-pane fade" id="favorites" role="tabpanel" aria-labelledby="favorites-tab">
        <!-- Favorite Streams content goes here -->
    </div>
    <div class="tab-pane fade" id="leaderboard" role="tabpanel" aria-labelledby="leaderboard-tab">
        <!-- LeaderBoard content goes here -->
    </div>
    <div class="tab-pane fade" id="about" role="tabpanel" aria-labelledby="about-tab">
        <!-- About content goes here -->
    </div>
</div>
```

### Key Changes:
1. **Button Elements**: Changed `<a>` tags to `<button>` elements for tab navigation, which is more appropriate for Bootstrap tabs.
2. **Data Attributes**: Added `data-bs-target` attributes to link each tab button to its corresponding content.
3. **Tab Content**: Added a `<div class="tab-content">` section to hold the content for each tab, with each tab pane having a unique ID that matches the `data-bs-target` of the corresponding button.
4. **Active Class**: The first tab is set to active by default.

Make sure to include Bootstrap's CSS and JS files in your project for the tabs to function correctly.