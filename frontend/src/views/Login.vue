<script setup>
import { computed, onMounted } from "vue";
import { useRouter } from "vue-router";
//import { useUserProfileStore } from "@/stores/userProfileStore";
import LoginButton from "@/components/LoginButton.vue";
import axios from "axios";

const router = useRouter();
/*
const userStore = useUserProfileStore();

// ログイン状態とユーザー情報を取得
const isLoggedIn = computed(() => userStore.isLoggedIn);
const displayName = computed(() => userStore.displayName);
const profileImageUrl = computed(() => userStore.profileImageUrl);

// 初期化処理: コンポーネントのマウント時にプロフィールを取得
onMounted(async () => {
  await userStore.fetchUserProfile();
  if (userStore.isLoggedIn) {
    try {
      const response = await axios.get(`/api/users/me`);
    } catch (error) {
      if (error.response && error.response.status === 404) {
        const postResponse = await axios.post("/api/users");
      } else {
        console.error("エラーが発生しました:", error);
      }
    }
  }
});
*/

// ボタンクリック時の処理
const handleClick = () => {
  router.push("/location");
};

const viewHistory = () => {
  router.push("/ichiran");
};
</script>


<template>
  <div class="gallery-container">
    <div class="gallery-wrapper">
      <img
        loading="lazy"
        src="@/assets/img/new_background.png"
        class="gallery-background"
        alt="背景画像(神社)"
      />
      <img
        loading="lazy"
        src="@/assets/img/background-shrine-alpha.png"
        class="gallery-overlay"
        alt="しめ縄"
      />

        <button
          class="oracle-button"
          @click="handleClick"
        >
          おみくじ<br/>取得
        </button>
        
    </div>
  </div>
</template>

<style scoped>
.gallery-container {
  background: linear-gradient(to bottom, #35ECBB, #FF9C12);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  width: 100%;
  height: 100vh; /* 高さを画面の縦幅に合わせる */
  margin: 0 auto;
}

.gallery-wrapper {
  display: flex;
  flex-direction: column;
  position: relative;
  width: 100%;
  height: 100%; /* 高さを画面の縦幅に合わせる */
}

.gallery-background,
.gallery-overlay {
  position: absolute;
  inset: 0;
  height: 100%;
  width: 100%;
  object-fit: cover;
}

.gallery-header {
  position: absolute;
  top: 130px !important; /* ロゴを少し下に配置 */
  left: 40px !important; /* ロゴを少し右に配置 */
  width: 200px!important; /* ロゴの幅を指定してサイズを大きくする */
  height: auto; /* 高さは自動で調整 */
  aspect-ratio: 1.22; /* アスペクト比を維持 */
  z-index: 10;
  max-width: 100%; /* 最大幅は100% */
}


.oracle-button {
  position: absolute;
  top: 60%; /* 縦の中央に配置 */
  left: 50%; /* 横の中央に配置 */
  transform: translate(-50%, -50%) scale(2); /* 中心揃え + 大きさ2倍 */
  background-image: url('@/assets/img/hisigata.png');
  background-size: cover;
  background-position: center;
  background-color: transparent;
  color: #000000;
  height: 12vh; /* 元の高さ */
  width: 12vh; /* 元の幅 */
  text-align: center;
  font-size: 20px;
  border: none;
  border-radius: 0;
  cursor: pointer;
  z-index: 20;
  font: inherit;

  /* 文字間隔調整 */
  letter-spacing: -1px; /* 文字間を狭める */
  /* 改行間隔の調整 */
  line-height: 1.1; /* 行間を狭くする */
}

.view-history-button {
  position: absolute;
  bottom: 5%; /* 下に配置 */
  left: 50%;
  transform: translateX(-50%);
  background-image: url('@/assets/img/location-header.png');
  background-size: cover;
  background-position: center;
  color: #fff;
  padding: 10px;
  width: 70%;
  text-align: center;
  font-size: 16px;
  border-radius: 12px;
  border: 2px solid rgba(255, 215, 0, 0.4);
  cursor: pointer;
  z-index: 10;
  font: inherit;
  line-height: 1.2; /* 行間を狭くする */
}

.view-history-button:hover,
.view-history-button:focus {
  background-color: #ff5722;
}

.login-button {
  position: absolute;
  z-index: 10;
  top: 70%;
  left: 50%;
  transform: translateX(-50%) scale(1.25);
}

@media (max-width: 600px) {
  .gallery-header {
    top: 20px; /* スマホでもロゴを少し下に配置 */
    left: 0;
    width: 40%; /* 小さな画面向けに幅を調整 */
  }

  .oracle-button,
  .view-history-button {
    font-size: 14px;
    height: 10vh;
    width: 10vh;
  }

  .login-button {
    transform: translateX(-50%) scale(1);
    bottom: 0px!important;
  }
}
</style>
