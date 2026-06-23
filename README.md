<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Feed My Belly — Build Your Family's Recipe Collection</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
 
  :root {
    --orange: #E8622A;
    --orange-light: #FDEEE4;
    --orange-mid: #F5DEC8;
    --cream: #FFF8F0;
    --dark: #222222;
    --mid: #555555;
    --light: #999999;
    --white: #FFFFFF;
    --green: #2D6A2D;
    --green-light: #F0F7F0;
  }
 
  body {
    font-family: 'Nunito', sans-serif;
    background: var(--cream);
    color: var(--dark);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
 
  /* HEADER */
  .header {
    background: var(--white);
    border-bottom: 2px solid var(--orange-mid);
    padding: 14px 24px;
    text-align: center;
  }
  .logo {
    font-size: 20px;
    font-weight: 900;
    color: var(--orange);
    letter-spacing: -0.5px;
  }
  .logo span { color: var(--dark); }
 
  /* PROGRESS BAR */
  .progress-wrap {
    background: var(--white);
    padding: 12px 24px 16px;
    border-bottom: 1px solid var(--orange-mid);
  }
  .progress-label {
    display: flex;
    justify-content: space-between;
    font-size: 12px;
    font-weight: 700;
    color: var(--light);
    margin-bottom: 8px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }
  .progress-label span:last-child { color: var(--orange); }
  .progress-bar {
    height: 6px;
    background: var(--orange-mid);
    border-radius: 100px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    background: var(--orange);
    border-radius: 100px;
    transition: width 0.4s ease;
  }
 
  /* MAIN CONTENT */
  .quiz-wrap {
    flex: 1;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    padding: 32px 24px 48px;
  }
 
  .screen {
    display: none;
    width: 100%;
    max-width: 580px;
    animation: fadeIn 0.3s ease;
  }
  .screen.active { display: block; }
 
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(12px); }
    to   { opacity: 1; transform: translateY(0); }
  }
 
  /* INTRO SCREEN */
  .intro-badge {
    display: inline-block;
    background: var(--orange-light);
    color: var(--orange);
    font-size: 12px;
    font-weight: 800;
    padding: 6px 16px;
    border-radius: 100px;
    margin-bottom: 20px;
    letter-spacing: 0.5px;
    text-transform: uppercase;
  }
  .intro-headline {
    font-size: clamp(28px, 6vw, 42px);
    font-weight: 900;
    line-height: 1.1;
    letter-spacing: -1px;
    margin-bottom: 16px;
    color: var(--dark);
  }
  .intro-headline em {
    font-style: normal;
    color: var(--orange);
  }
  .intro-sub {
    font-size: 17px;
    color: var(--mid);
    line-height: 1.6;
    margin-bottom: 28px;
  }
  .intro-meta {
    display: flex;
    gap: 20px;
    margin-bottom: 32px;
    flex-wrap: wrap;
  }
  .intro-meta-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 14px;
    font-weight: 700;
    color: var(--mid);
  }
  .intro-meta-item .dot {
    width: 8px; height: 8px;
    background: var(--orange);
    border-radius: 50%;
    flex-shrink: 0;
  }
 
  /* QUESTION SCREEN */
  .q-step {
    font-size: 12px;
    font-weight: 800;
    color: var(--orange);
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 10px;
  }
  .q-headline {
    font-size: clamp(22px, 4vw, 30px);
    font-weight: 900;
    line-height: 1.2;
    letter-spacing: -0.5px;
    margin-bottom: 8px;
    color: var(--dark);
  }
  .q-sub {
    font-size: 14px;
    color: var(--light);
    margin-bottom: 24px;
  }
 
  /* OPTIONS */
  .options-grid {
    display: grid;
    gap: 12px;
    margin-bottom: 28px;
  }
  .options-grid.cols-2 { grid-template-columns: 1fr 1fr; }
  .options-grid.cols-1 { grid-template-columns: 1fr; }
 
  .option {
    background: var(--white);
    border: 2px solid var(--orange-mid);
    border-radius: 14px;
    padding: 16px 18px;
    cursor: pointer;
    transition: all 0.15s;
    display: flex;
    align-items: center;
    gap: 14px;
    text-align: left;
    width: 100%;
    font-family: 'Nunito', sans-serif;
  }
  .option:hover {
    border-color: var(--orange);
    background: var(--orange-light);
  }
  .option.selected {
    border-color: var(--orange);
    background: var(--orange-light);
  }
  .option-icon {
    font-size: 24px;
    flex-shrink: 0;
    width: 36px;
    text-align: center;
  }
  .option-text { flex: 1; }
  .option-label {
    font-size: 15px;
    font-weight: 800;
    color: var(--dark);
    display: block;
    margin-bottom: 2px;
  }
  .option-desc {
    font-size: 12px;
    color: var(--light);
    font-weight: 400;
  }
  .option-check {
    width: 22px; height: 22px;
    border: 2px solid var(--orange-mid);
    border-radius: 50%;
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.15s;
  }
  .option.selected .option-check {
    background: var(--orange);
    border-color: var(--orange);
  }
  .option.selected .option-check::after {
    content: '';
    width: 5px; height: 9px;
    border: 2px solid white;
    border-top: none;
    border-left: none;
    transform: rotate(45deg) translateY(-1px);
    display: block;
  }
 
  /* CHECKBOX OPTIONS (multi-select) */
  .checkbox-option .option-check {
    border-radius: 6px;
  }
 
  /* BUTTONS */
  .btn-primary {
    display: block;
    width: 100%;
    background: var(--orange);
    color: var(--white);
    font-family: 'Nunito', sans-serif;
    font-size: 17px;
    font-weight: 800;
    padding: 18px 32px;
    border-radius: 100px;
    border: none;
    cursor: pointer;
    text-align: center;
    text-decoration: none;
    transition: background 0.15s;
    line-height: 1;
  }
  .btn-primary:hover { background: #C04E18; }
  .btn-primary:disabled {
    background: var(--orange-mid);
    color: var(--light);
    cursor: not-allowed;
  }
  .btn-back {
    background: none;
    border: none;
    color: var(--light);
    font-family: 'Nunito', sans-serif;
    font-size: 14px;
    font-weight: 700;
    cursor: pointer;
    padding: 12px 0;
    display: block;
    text-align: center;
    width: 100%;
    margin-top: 8px;
  }
  .btn-back:hover { color: var(--mid); }
 
  /* RESULTS SCREEN */
  .results-header {
    background: var(--orange);
    border-radius: 20px;
    padding: 28px 24px;
    text-align: center;
    margin-bottom: 24px;
  }
  .results-header h2 {
    font-size: 24px;
    font-weight: 900;
    color: var(--white);
    margin-bottom: 8px;
    line-height: 1.2;
  }
  .results-header p {
    font-size: 14px;
    color: rgba(255,255,255,0.85);
    line-height: 1.5;
  }
 
  .results-summary {
    background: var(--white);
    border: 2px solid var(--orange-mid);
    border-radius: 16px;
    padding: 20px;
    margin-bottom: 20px;
  }
  .results-summary h3 {
    font-size: 13px;
    font-weight: 800;
    color: var(--orange);
    text-transform: uppercase;
    letter-spacing: 0.5px;
    margin-bottom: 14px;
  }
  .summary-item {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 10px 0;
    border-bottom: 1px solid var(--orange-mid);
    font-size: 14px;
  }
  .summary-item:last-child { border-bottom: none; padding-bottom: 0; }
  .summary-label {
    font-weight: 700;
    color: var(--mid);
    min-width: 120px;
    flex-shrink: 0;
  }
  .summary-value {
    color: var(--dark);
    font-weight: 600;
    flex: 1;
  }
 
  .results-includes {
    background: var(--green-light);
    border-radius: 16px;
    padding: 20px;
    margin-bottom: 24px;
  }
  .results-includes h3 {
    font-size: 13px;
    font-weight: 800;
    color: var(--green);
    text-transform: uppercase;
    letter-spacing: 0.5px;
    margin-bottom: 14px;
  }
  .includes-item {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 14px;
    font-weight: 700;
    color: var(--dark);
    padding: 5px 0;
  }
  .includes-dot {
    width: 8px; height: 8px;
    background: var(--green);
    border-radius: 50%;
    flex-shrink: 0;
  }
 
  .price-reveal {
    text-align: center;
    margin-bottom: 20px;
  }
  .price-reveal .founding {
    display: inline-block;
    background: var(--orange);
    color: var(--white);
    font-size: 13px;
    font-weight: 800;
    padding: 8px 18px;
    border-radius: 100px;
    margin-bottom: 12px;
  }
  .price-reveal .price-line {
    font-size: 42px;
    font-weight: 900;
    color: var(--orange);
    line-height: 1;
    margin-bottom: 4px;
  }
  .price-reveal .price-line sup { font-size: 20px; vertical-align: super; }
  .price-reveal .price-line sub { font-size: 16px; color: var(--light); font-weight: 600; }
  .price-reveal .price-was {
    font-size: 14px;
    color: var(--light);
    text-decoration: line-through;
    margin-bottom: 4px;
  }
  .price-reveal .price-note {
    font-size: 13px;
    color: var(--mid);
  }
 
  .trust-row {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-top: 14px;
    flex-wrap: wrap;
  }
  .trust-item {
    font-size: 12px;
    font-weight: 700;
    color: var(--light);
    display: flex;
    align-items: center;
    gap: 5px;
  }
 
  /* FOOTER */
  .footer {
    background: var(--dark);
    color: var(--light);
    text-align: center;
    padding: 16px 24px;
    font-size: 12px;
  }
  .footer a { color: #bbb; text-decoration: none; }
 
  @media (max-width: 480px) {
    .options-grid.cols-2 { grid-template-columns: 1fr; }
    .intro-meta { gap: 12px; }
  }
</style>
</head>
<body>
 
<div class="header">
  <div class="logo">Feed My <span>Belly</span> 🍽️</div>
</div>
 
<div class="progress-wrap" id="progressWrap" style="display:none;">
  <div class="progress-label">
    <span>Building your recipe collection</span>
    <span id="progressText">1 of 7</span>
  </div>
  <div class="progress-bar">
    <div class="progress-fill" id="progressFill" style="width:14%"></div>
  </div>
</div>
 
<div class="quiz-wrap">
 
  <!-- INTRO -->
  <div class="screen active" id="screen-intro">
    <div class="intro-badge">Takes less than 2 minutes</div>
    <h1 class="intro-headline">Let's build your family's <em>perfect</em> recipe collection.</h1>
    <p class="intro-sub">Answer 7 quick questions and we'll show you exactly what your custom weekly collection will look like — built around your family, your schedule, and your goals.</p>
    <div class="intro-meta">
      <div class="intro-meta-item"><span class="dot"></span> 100% custom for your family</div>
      <div class="intro-meta-item"><span class="dot"></span> Delivered every Friday</div>
      <div class="intro-meta-item"><span class="dot"></span> First 7 days free</div>
    </div>
    <button class="btn-primary" onclick="startQuiz()">Build My Recipe Collection →</button>
  </div>
 
  <!-- Q1: Who are you cooking for? -->
  <div class="screen" id="screen-1">
    <div class="q-step">Question 1 of 7</div>
    <h2 class="q-headline">Who are you cooking for?</h2>
    <p class="q-sub">We'll tailor every recipe to the right number of people and ages.</p>
    <div class="options-grid cols-2" id="q1-options">
      <button class="option" onclick="selectOption(this, 'q1', 'Just me')" data-value="Just me">
        <span class="option-icon">🧑</span>
        <span class="option-text"><span class="option-label">Just me</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q1', 'Me & my partner')" data-value="Me & my partner">
        <span class="option-icon">👫</span>
        <span class="option-text"><span class="option-label">Me & my partner</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q1', 'Family with kids')" data-value="Family with kids">
        <span class="option-icon">👨‍👩‍👧</span>
        <span class="option-text"><span class="option-label">Family with kids</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q1', 'Family without kids')" data-value="Family without kids">
        <span class="option-icon">🏠</span>
        <span class="option-text"><span class="option-label">Family, no kids</span></span>
        <span class="option-check"></span>
      </button>
    </div>
    <button class="btn-primary" id="next-1" onclick="nextScreen(2)" disabled>Next →</button>
    <button class="btn-back" onclick="goBack(0)">← Back</button>
  </div>
 
  <!-- Q2: How many people? -->
  <div class="screen" id="screen-2">
    <div class="q-step">Question 2 of 7</div>
    <h2 class="q-headline">How many people are you feeding?</h2>
    <p class="q-sub">We'll make sure portions and grocery lists are always right.</p>
    <div class="options-grid cols-2" id="q2-options">
      <button class="option" onclick="selectOption(this, 'q2', '1-2 people')" data-value="1-2 people">
        <span class="option-icon">🍽️</span>
        <span class="option-text"><span class="option-label">1–2 people</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q2', '3-4 people')" data-value="3-4 people">
        <span class="option-icon">🍽️🍽️</span>
        <span class="option-text"><span class="option-label">3–4 people</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q2', '5-6 people')" data-value="5-6 people">
        <span class="option-icon">🍽️🍽️🍽️</span>
        <span class="option-text"><span class="option-label">5–6 people</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q2', '7+ people')" data-value="7+ people">
        <span class="option-icon">🏡</span>
        <span class="option-text"><span class="option-label">7+ people</span></span>
        <span class="option-check"></span>
      </button>
    </div>
    <button class="btn-primary" id="next-2" onclick="nextScreen(3)" disabled>Next →</button>
    <button class="btn-back" onclick="goBack(1)">← Back</button>
  </div>
 
  <!-- Q3: Biggest dinner struggle -->
  <div class="screen" id="screen-3">
    <div class="q-step">Question 3 of 7</div>
    <h2 class="q-headline">What's your biggest struggle at dinnertime?</h2>
    <p class="q-sub">Pick the one that hits closest to home.</p>
    <div class="options-grid cols-1" id="q3-options">
      <button class="option" onclick="selectOption(this, 'q3', 'No time to cook')" data-value="No time to cook">
        <span class="option-icon">⏱️</span>
        <span class="option-text">
          <span class="option-label">No time to cook</span>
          <span class="option-desc">Weeknights are chaos — I need fast meals</span>
        </span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q3', 'No ideas')" data-value="No ideas">
        <span class="option-icon">🤷</span>
        <span class="option-text">
          <span class="option-label">I run out of ideas</span>
          <span class="option-desc">We keep making the same 5 meals on repeat</span>
        </span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q3', 'Picky eaters')" data-value="Picky eaters">
        <span class="option-icon">😤</span>
        <span class="option-text">
          <span class="option-label">Picky eaters</span>
          <span class="option-desc">Getting everyone to eat the same thing is a battle</span>
        </span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q3', 'Unhealthy habits')" data-value="Unhealthy habits">
        <span class="option-icon">🍕</span>
        <span class="option-text">
          <span class="option-label">Too much takeout</span>
          <span class="option-desc">We end up ordering in more than I'd like</span>
        </span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q3', 'Budget')" data-value="Budget">
        <span class="option-icon">💰</span>
        <span class="option-text">
          <span class="option-label">Staying on budget</span>
          <span class="option-desc">Groceries add up fast without a plan</span>
        </span>
        <span class="option-check"></span>
      </button>
    </div>
    <button class="btn-primary" id="next-3" onclick="nextScreen(4)" disabled>Next →</button>
    <button class="btn-back" onclick="goBack(2)">← Back</button>
  </div>
 
  <!-- Q4: Meal style -->
  <div class="screen" id="screen-4">
    <div class="q-step">Question 4 of 7</div>
    <h2 class="q-headline">What kind of meals does your family love?</h2>
    <p class="q-sub">Your collection will be full of meals everyone actually looks forward to.</p>
    <div class="options-grid cols-2" id="q4-options">
      <button class="option" onclick="selectOption(this, 'q4', 'Quick & easy')" data-value="Quick & easy">
        <span class="option-icon">⚡</span>
        <span class="option-text"><span class="option-label">Quick & easy</span><span class="option-desc">30 min or less</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q4', 'Comfort food')" data-value="Comfort food">
        <span class="option-icon">🥘</span>
        <span class="option-text"><span class="option-label">Comfort food</span><span class="option-desc">Hearty, satisfying meals</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q4', 'Healthy & fresh')" data-value="Healthy & fresh">
        <span class="option-icon">🥗</span>
        <span class="option-text"><span class="option-label">Healthy & fresh</span><span class="option-desc">Light, nutritious choices</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q4', 'Mix of everything')" data-value="Mix of everything">
        <span class="option-icon">🌮</span>
        <span class="option-text"><span class="option-label">Mix of everything</span><span class="option-desc">Variety keeps it interesting</span></span>
        <span class="option-check"></span>
      </button>
    </div>
    <button class="btn-primary" id="next-4" onclick="nextScreen(5)" disabled>Next →</button>
    <button class="btn-back" onclick="goBack(3)">← Back</button>
  </div>
 
  <!-- Q5: Dietary needs -->
  <div class="screen" id="screen-5">
    <div class="q-step">Question 5 of 7</div>
    <h2 class="q-headline">Any dietary needs we should know about?</h2>
    <p class="q-sub">Select all that apply — we'll build around them, not around them.</p>
    <div class="options-grid cols-2" id="q5-options">
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q5', 'None')" data-value="None">
        <span class="option-icon">✅</span>
        <span class="option-text"><span class="option-label">No restrictions</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q5', 'Gluten-free')" data-value="Gluten-free">
        <span class="option-icon">🌾</span>
        <span class="option-text"><span class="option-label">Gluten-free</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q5', 'Dairy-free')" data-value="Dairy-free">
        <span class="option-icon">🥛</span>
        <span class="option-text"><span class="option-label">Dairy-free</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q5', 'Vegetarian')" data-value="Vegetarian">
        <span class="option-icon">🥦</span>
        <span class="option-text"><span class="option-label">Vegetarian</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q5', 'Nut allergy')" data-value="Nut allergy">
        <span class="option-icon">🥜</span>
        <span class="option-text"><span class="option-label">Nut allergy</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q5', 'Other allergy')" data-value="Other allergy">
        <span class="option-icon">⚠️</span>
        <span class="option-text"><span class="option-label">Other allergy</span></span>
        <span class="option-check"></span>
      </button>
    </div>
    <button class="btn-primary" id="next-5" onclick="nextScreen(6)" disabled>Next →</button>
    <button class="btn-back" onclick="goBack(4)">← Back</button>
  </div>
 
  <!-- Q6: Cook time -->
  <div class="screen" id="screen-6">
    <div class="q-step">Question 6 of 7</div>
    <h2 class="q-headline">How much time do you have to cook on a typical weeknight?</h2>
    <p class="q-sub">We'll match every recipe to your real life — not some ideal version of it.</p>
    <div class="options-grid cols-1" id="q6-options">
      <button class="option" onclick="selectOption(this, 'q6', 'Under 15 min')" data-value="Under 15 min">
        <span class="option-icon">⚡</span>
        <span class="option-text"><span class="option-label">Under 15 minutes</span><span class="option-desc">I need things on the table fast</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q6', '15-30 min')" data-value="15-30 min">
        <span class="option-icon">🕐</span>
        <span class="option-text"><span class="option-label">15–30 minutes</span><span class="option-desc">Quick but not rushed</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q6', '30-45 min')" data-value="30-45 min">
        <span class="option-icon">🕑</span>
        <span class="option-text"><span class="option-label">30–45 minutes</span><span class="option-desc">I can do a proper cook</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option" onclick="selectOption(this, 'q6', 'I love cooking')" data-value="I love cooking">
        <span class="option-icon">👨‍🍳</span>
        <span class="option-text"><span class="option-label">I love cooking</span><span class="option-desc">Time isn't an issue — give me real recipes</span></span>
        <span class="option-check"></span>
      </button>
    </div>
    <button class="btn-primary" id="next-6" onclick="nextScreen(7)" disabled>Next →</button>
    <button class="btn-back" onclick="goBack(5)">← Back</button>
  </div>
 
  <!-- Q7: Health & fitness goals -->
  <div class="screen" id="screen-7">
    <div class="q-step">Question 7 of 7</div>
    <h2 class="q-headline">Any health or fitness goals we should build around?</h2>
    <p class="q-sub">Select all that apply — we'll factor these into your recipes.</p>
    <div class="options-grid cols-2" id="q7-options">
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'Heart health')" data-value="Heart health">
        <span class="option-icon">❤️</span>
        <span class="option-text"><span class="option-label">Heart health</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'Weight management')" data-value="Weight management">
        <span class="option-icon">⚖️</span>
        <span class="option-text"><span class="option-label">Weight management</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'Energy & mood')" data-value="Energy & mood">
        <span class="option-icon">⚡</span>
        <span class="option-text"><span class="option-label">Energy & mood</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'Digestive health')" data-value="Digestive health">
        <span class="option-icon">🌿</span>
        <span class="option-text"><span class="option-label">Digestive health</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'Kids nutrition')" data-value="Kids nutrition">
        <span class="option-icon">👶</span>
        <span class="option-text"><span class="option-label">Kids nutrition</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'High protein')" data-value="High protein">
        <span class="option-icon">💪</span>
        <span class="option-text"><span class="option-label">High protein</span><span class="option-desc">Weight lifting / strength</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'Endurance & performance')" data-value="Endurance & performance">
        <span class="option-icon">🏃</span>
        <span class="option-text"><span class="option-label">Endurance & performance</span><span class="option-desc">Running / cardio</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'Low carb')" data-value="Low carb">
        <span class="option-icon">🥩</span>
        <span class="option-text"><span class="option-label">Low carb</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'General wellness')" data-value="General wellness">
        <span class="option-icon">🌟</span>
        <span class="option-text"><span class="option-label">General wellness</span></span>
        <span class="option-check"></span>
      </button>
      <button class="option checkbox-option" onclick="toggleCheckbox(this, 'q7', 'No specific goals')" data-value="No specific goals">
        <span class="option-icon">😊</span>
        <span class="option-text"><span class="option-label">No specific goals</span></span>
        <span class="option-check"></span>
      </button>
    </div>
    <button class="btn-primary" id="next-7" onclick="showResults()" disabled>See My Recipe Collection →</button>
    <button class="btn-back" onclick="goBack(6)">← Back</button>
  </div>
 
  <!-- RESULTS -->
  <div class="screen" id="screen-results">
    <div class="results-header">
      <h2>🎉 Your recipe collection is ready!</h2>
      <p>Based on your answers, here's exactly what we'll build for you every single Friday.</p>
    </div>
 
    <div class="results-summary">
      <h3>Your personalised plan</h3>
      <div id="summary-content">
        <!-- populated by JS -->
      </div>
    </div>
 
    <div class="results-includes">
      <h3>What's in your collection every week</h3>
      <div class="includes-item"><span class="includes-dot"></span> 7 days of breakfasts, lunches, dinners & snacks</div>
      <div class="includes-item"><span class="includes-dot"></span> Recipes matched to your cook time & skill level</div>
      <div class="includes-item"><span class="includes-dot"></span> A ready-to-use grocery list, sorted by store section</div>
      <div class="includes-item"><span class="includes-dot"></span> Built around your dietary needs & health goals</div>
      <div class="includes-item"><span class="includes-dot"></span> Delivered every Friday before your week begins</div>
    </div>
 
    <div class="price-reveal">
      <div class="founding">🎉 Founding Member — Code FOUNDING50 · Expires June 30</div>
      <div class="price-was">Regular price $37/month</div>
      <div class="price-line"><sup>$</sup>18.50<sub>/mo</sub></div>
      <div class="price-note">After your free 7-day trial · 50% off, locked in · Cancel anytime</div>
    </div>
 
    <a href="https://www.feedmybelly.net/order" class="btn-primary">Start My Free 7-Day Trial →</a>
 
    <div class="trust-row">
      <span class="trust-item">✓ No charge for 7 days</span>
      <span class="trust-item">✓ Cancel anytime</span>
      <span class="trust-item">✓ No commitment</span>
    </div>
  </div>
 
</div><!-- end quiz-wrap -->
 
<div class="footer">
  © 2026 Feed My Belly · <a href="mailto:sandra@feedmybelly.net">sandra@feedmybelly.net</a> ·
  <a href="#">Privacy Policy</a>
</div>
 
<script>
  // Store answers
  const answers = {
    q1: null, q2: null, q3: null, q4: null,
    q5: [], q6: null, q7: []
  };
 
  const totalQuestions = 7;
 
  function startQuiz() {
    showScreen('screen-1');
    document.getElementById('progressWrap').style.display = 'block';
    updateProgress(1);
  }
 
  function showScreen(id) {
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    window.scrollTo(0, 0);
  }
 
  function updateProgress(step) {
    const pct = Math.round((step / totalQuestions) * 100);
    document.getElementById('progressFill').style.width = pct + '%';
    document.getElementById('progressText').textContent = step + ' of ' + totalQuestions;
  }
 
  // Single select
  function selectOption(el, key, value) {
    const container = el.closest('.options-grid');
    container.querySelectorAll('.option').forEach(o => o.classList.remove('selected'));
    el.classList.add('selected');
    answers[key] = value;
    const stepNum = key.replace('q', '');
    document.getElementById('next-' + stepNum).disabled = false;
  }
 
  // Multi select (checkboxes)
  function toggleCheckbox(el, key, value) {
    el.classList.toggle('selected');
    if (el.classList.contains('selected')) {
      if (!answers[key].includes(value)) answers[key].push(value);
    } else {
      answers[key] = answers[key].filter(v => v !== value);
    }
    const stepNum = key.replace('q', '');
    const nextBtn = document.getElementById('next-' + stepNum);
    if (nextBtn) nextBtn.disabled = answers[key].length === 0;
  }
 
  function nextScreen(step) {
    showScreen('screen-' + step);
    updateProgress(step);
  }
 
  function goBack(step) {
    if (step === 0) {
      showScreen('screen-intro');
      document.getElementById('progressWrap').style.display = 'none';
    } else {
      showScreen('screen-' + step);
      updateProgress(step);
    }
  }
 
  function showResults() {
    // Build summary
    const goalsList = answers.q7.length > 0 ? answers.q7.join(', ') : 'General wellness';
    const dietList = answers.q5.length > 0 ? answers.q5.join(', ') : 'No restrictions';
 
    const summaryItems = [
      { label: 'Cooking for', value: answers.q1 },
      { label: 'Servings', value: answers.q2 },
      { label: 'Main challenge', value: answers.q3 },
      { label: 'Meal style', value: answers.q4 },
      { label: 'Dietary needs', value: dietList },
      { label: 'Cook time', value: answers.q6 },
      { label: 'Health goals', value: goalsList },
    ];
 
    const html = summaryItems.map(item => `
      <div class="summary-item">
        <span class="summary-label">${item.label}</span>
        <span class="summary-value">${item.value}</span>
      </div>
    `).join('');
 
    document.getElementById('summary-content').innerHTML = html;
 
    showScreen('screen-results');
    document.getElementById('progressWrap').style.display = 'none';
    window.scrollTo(0, 0);
  }
</script>
 
</body>
</html>
