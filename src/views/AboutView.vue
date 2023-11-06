<template>
  <div class="about">
    <h1>A social club for casual and competitive chess</h1>
    <p>
      The Victoria University of Wellington Chess Club is a place for chess enthusiasts to come
      together, share their love for the game, and have a good time. No matter your skill level,
      you're invited to be a part of the community.
    </p>
    <p>
      Our weekly meetups offer a space to enjoy casual over-the-board chess matches and work
      together on solving chess puzzles. It's all about the joy of playing and learning from one
      another.
    </p>
    <p>
      Feel free to join us at the chess club for some enjoyable games. We've got boards and clocks
      ready for you, but if you prefer your own gear, don't hesitate to bring it along.
    </p>
  </div>
</template>

<style>
.about {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: var(--background-color);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  border-radius: 25px;
  padding: 1rem 1rem 2rem 1rem;
}

.about p {
  margin-top: 1rem;
}

@media (min-width: 1024px) {
  .about h1 {
    font-weight: 500;
    font-size: 2rem;
  }
}
</style>
