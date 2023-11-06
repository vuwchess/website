<script setup lang="ts">
import WelcomeItem from './WelcomeItem.vue'
import DiscordIcon from './icons/IconDiscord.vue'
import OnlineChessIcon from './icons/IconOnlineChess.vue'
import ContactIcon from './icons/IconContact.vue'
</script>

<template>
  <div class="welcome-wrapper">
    <WelcomeItem>
      <template #icon>
        <DiscordIcon />
      </template>
      <template #heading>Discord</template>

      Join our <a href="https://discord.gg/pCg4WWxk8E" target="_blank" rel="noopener">discord server</a> to chat with
      other
      members of
      the club and to keep up with the latest news and events.
    </WelcomeItem>

    <WelcomeItem>
      <template #icon>
        <OnlineChessIcon />
      </template>
      <template #heading>Online Chess</template>

      Join our <a href="https://www.chess.com/club/vuw-chess-club/join/cac54e">Chess.com club</a> to play online chess
      with
      other members of the club. We also have a
      <a href="https://lichess.org/team/vuw-chess-club" target="_blank" rel="noopener">Lichess.org team</a>.

    </WelcomeItem>

    <WelcomeItem>
      <template #icon>
        <ContactIcon />
      </template>
      <template #heading>Contact</template>

      Feel free to contact us at
      <a href="mailto:vuwchess@gmail.com" type="email" target="_blank" rel="noopener">vuwchess@gmail.com</a> for any
      questions or queries.
    </WelcomeItem>
  </div>
</template>

<style scoped>
.welcome-wrapper {
  padding: 1rem 2rem;
}
</style>
