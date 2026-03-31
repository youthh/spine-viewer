<template>
  <div v-if="visible" class="redirect-overlay">
    <div class="content">
      <h1>⚠️ This app is not supported anymore</h1>

      <p class="subtitle">
        We’ve moved on... and so should you 😄
      </p>

      <p class="farewell">
        До побачення 👋 See you on the new version!
      </p>

      <div class="countdown">
        Redirecting in <span>{{ countdown }}</span>...
      </div>

      <button @click="redirectNow">
        Take me there 🚀
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppRedirectNotice',

  props: {
    delay: {
      type: Number,
      default: 4000,
    },
    url: {
      type: String,
      required: true,
    },
  },

  data() {
    return {
      visible: true,
      countdown: Math.ceil(this.delay / 1000),
      interval: null,
    };
  },

  mounted() {
    this.interval = setInterval(() => {
      if (this.countdown > 0) {
        this.countdown -= 1;
      }
    }, 1000);

    setTimeout(() => {
      this.redirectNow();
    }, this.delay);
  },

  beforeDestroy() {
    clearInterval(this.interval);
  },

  methods: {
    redirectNow() {
      window.location.href = this.url;
    },
  },
};
</script>

<style scoped>
.redirect-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at center, #1e293b, #020617);
  color: white;

  display: flex;
  justify-content: center;
  align-items: center;

  z-index: 9999;
  animation: fadeIn 0.5s ease;
}

.content {
  text-align: center;
  max-width: 400px;
}

h1 {
  font-size: 28px;
  margin-bottom: 10px;
}

.subtitle {
  opacity: 0.8;
  margin-bottom: 10px;
}

.farewell {
  font-size: 18px;
  margin-bottom: 20px;
  color: #38bdf8;
}

.countdown {
  font-size: 20px;
  margin-bottom: 20px;
}

.countdown span {
  font-size: 28px;
  font-weight: bold;
  color: #4a86c7;
}

button {
  padding: 10px 20px;
  border: none;
  background: #4a86c7;
  color: white;
  cursor: pointer;
  border-radius: 8px;
  transition: 0.2s;
}

button:hover {
  background: #3a6fa5;
  transform: scale(1.05);
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
