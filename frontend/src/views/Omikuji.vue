<template>
  <div class="result-screen">
    <div class="result-container">
      <img
        loading="lazy"
        src="https://cdn.builder.io/api/v1/image/assets/TEMP/5e81f6d4ca789c8e3f9077e0b717f7c8b773568f91ec42fd69779d2e78a5813b?placeholderIfAbsent=true&apiKey=d15c8345fe15403fbf2733b286d943d4"
        class="background-image"
        alt=""
      />
      <div class="fortune-display">
        <img v-if="blobUrl" :src="blobUrl" alt="Generated Omikuji" />
        <button class="print-button" @click="handlePrint">
          🖨️ 印刷する
        </button>
        
        <!--<div>NFT Details</div>
        <div class="container unified-box">
          <div>
            <strong>Token ID:</strong> <span id="var1"></span>
          </div>
          <div>
            <strong>Blockchain:</strong> Polygon
          </div>
          <div>
            <strong>Token Standard:</strong> ERC-72
          </div>
          <div>
            <strong>Contract Address:</strong> 0xfB40b73E6cEe109Ae7614e621ffA841Dd1EB1584
          </div>
          <div>
            <strong>Transaction Hash:</strong> <span id="var2"></span>
          </div>
        </div>-->
      </div>
      <!--<div class="share-section">
        <button
          class="share-button"
          tabindex="0"
          @click="handleShare"
          aria-label="おみくじをシェア">
          <span>おみくじをシェア</span>
        </button>-->
        <!--<img
          loading="lazy"
          src="https://cdn.builder.io/api/v1/image/assets/TEMP/1b3025bf1577dd0e3f2ae1f42ff1ae5f416bca32090785e1241417b7bc11443d?placeholderIfAbsent=true&apiKey=d15c8345fe15403fbf2733b286d943d4"
          class="share-icon"
          alt="Share fortune result"
        />--->
      <!--</div>--->
      <button
         class="return-button"
         tabindex="0"
         @click="handleReturn"
         aria-label="最初へ戻る">
        <img
          loading="lazy"
          src="https://cdn.builder.io/api/v1/image/assets/TEMP/37658439fc1d41fe43bdb43b169f19d1626b20f05a953ebe1668ba8a62c7f442?placeholderIfAbsent=true&apiKey=d15c8345fe15403fbf2733b286d943d4"
          class="return-icon"
          alt=""
        />
        <span class="return-text">最初に戻る</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRouter, useRoute } from "vue-router";
import axios from "axios";

const router = useRouter();
const route = useRoute();
const omikujiText = ref({});//ami
const picture = "https://tyoudoii-illust.com/wp-content/uploads/2024/07/oksign_businessman_simple-300x282.png";

const omikuziText = {
  "運勢": "大吉",
  "願望": "多くの思いを乗せ...",
  "健康": "日々の生活を整えれば...",
  "金運": "自分の強みを活かして...",
  "学問": "劇的にして...",
  "恋愛": "信じ合うこと離に打ち勝て...",
  "神託": "一輝よ、朝の目覚めに新たな環境で暮らすと..."
};

const blobUrl = ref(null);


onMounted(()=>{
  const{photo, omikuji }=route.query; //ami omikuji
  blobUrl.value=photo;
  
  // おみくじのJSON文字列を正しくパースする
  if (typeof omikuji === "string") {
    try {
      omikujiText.value = JSON.parse(decodeURIComponent(omikuji));
      console.log("パースされたomikujiText:", omikujiText.value);
      console.log("運勢:", omikujiText.value["運勢"]);
    } catch (e) {
      console.error("おみくじテキストのパースに失敗しました:", e);
      // オプションでomikujiTextのデフォルト値またはエラー状態を設定
      omikujiText.value = {
        "運勢": "N/A",
        "願望": "情報が取得できませんでした。",
        "健康": "情報が取得できませんでした。",
        "金運": "情報が取得できませんでした。",
        "学問": "情報が取得できませんでした。",
        "恋愛": "情報が取得できませんでした。",
        "神託": "情報が取得できませんでした。"
      };
    }
  } else {
    console.warn("おみくじクエリパラメータが見つからないか、文字列ではありません。");
    // オプションでデフォルト値またはエラー状態を設定
    omikujiText.value = {
      "運勢": "N/A",
      "願望": "情報が取得できませんでした。",
      "健康": "情報が取得できませんでした。",
      "金運": "情報が取得できませんでした。",
      "学問": "情報が取得できませんでした。",
      "恋愛": "情報が取得できませんでした。",
      "神託": "情報が取得できませんでした。"
    };
  }  
  
  //console.log("Omikuji", omikuji);
  //omikujiText.value=omikuji;
  //omikujiText.value = JSON.parse(decodeURIComponent(omikuji));
  //console.log("OmikujiText.value", omikuji);
  //console.log("unsei:", omikujiText.value["運勢"]);
  // おみくじテキストの受け取り・デコード
  /*if (typeof omikuji === "string") {
    try {
      omikujiText.value = JSON.parse(decodeURIComponent(omikuji));
    } catch (e) {
      console.error("おみくじテキストの復元に失敗しました:", e);
    }
  } else {
    console.warn("omikujiクエリが存在しません");
  }
  /*if (typeof omikuji === "string") {
    const decoded = decodeURIComponent(omikuji);
    omikujiText.value = decoded; // ここでは string として扱う
  }*/
});
/*onMounted(async () => {
  try {
    console.log(route.query)

    const photo = route.query;
    /*const {photo, tokenId, transactionHash} = route.query;*/
    //blobUrl.value=photo;
    /*document.getElementById("var1").textContent = tokenId;ttm*/
    /*document.getElementById("var2").textContent = transactionHash;ttm*/
    
    /*console.log("NFT Token ID:", tokenId);ttm
  } catch (error) {
    console.error("エラーが発生しました:", error);
  }
});*/
/*const handleShare = async () => {
  try {
    if (navigator.share) {
      console.log("Blob URL:", blobUrl.value);

      const shareMessage = `友達にシェアしよう！画像はこちら: ${blobUrl.value}`;
      await navigator.share({
        title: "おみくじ結果",
        text: shareMessage,
      });
      console.log("シェア成功！");
    } else {
      alert("このブラウザではシェア機能がサポートされていません。");
    }
  } catch (error) {
    console.error("シェアエラー:", error);
  }
};*/



const handleReturn = () => {
  router.push("/");
};

const handlePrint = () => {
  const content = `
    <div style="font-family: sans-serif; padding: 20px; font-size: 10px;">
      <h1 style="text-align:center;">おみくじ結果</h1>
      <p><strong>運勢：</strong>${omikujiText.value["運勢"] || 'N/A'}</p>
      <p><strong>神託：</strong>${omikujiText.value["神託"] || 'N/A'}</p>
    </div>
  `;

  const printWindow = window.open('', '_blank');
  if (!printWindow) {
    alert("ポップアップブロックを解除してください");
    return;
  }

  printWindow.document.write(`
    <html>
      <head>
        <title>おみくじ印刷</title>
        <style>
          body {
            margin: 0;
            padding: 0;
          }
        </style>
      </head>
      <body>${content}</body>
    </html>
  `);
  printWindow.document.close();
  printWindow.focus();
  printWindow.print();
};

</script>

<style scoped>
.result-screen {
  background-color: rgba(245, 239, 219, 1);
  display: flex;
  max-width: 480px;
  width: 100%;
  flex-direction: column;
  overflow: hidden;
  color: rgba(0, 0, 0, 1);
  font-weight: 400;
  text-align: center;
  margin: 0 auto;
}

.result-container {
  display: flex;
  flex-direction: column;
  position: relative;
  aspect-ratio: 0.461;
  width: 100%;
  padding: 174px 0 27px;
}

.background-image {
  position: absolute;
  inset: 0;
  height: 100%;
  width: 100%;
  object-fit: cover;
  object-position: center;
}

.fortune-display {
  position: relative;
  display: flex;
  min-height: 395px;
  width: 100%;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  align-items: center; /* 中央寄せ */
  margin-bottom: 20px; /* fortune-displayの下に間隔を追加 */
}

.fortune-display img {
  max-width: 100%;
  height: auto;
  object-fit: contain;
}

.share-section {
  position: relative;
  display: flex;
  gap: 11px;
  font-size: 40px;
  align-items: center; /* 子要素の縦方向を中央揃え */
}

.share-section {
  position: relative;
  display: flex;
  gap: 11px;
  font-size: 40px;
  align-items: center; /* 子要素の縦方向を中央揃え */
  margin-top: 20px; /* 追加: share-sectionの上に間隔を追加 */
  right: -15px;
  top: -10px;
}

/*.share-button {
  align-self: center;
  flex-grow: 1;
  flex-basis: auto;
  border: none;
  background: none;
  cursor: pointer;
  font-family: inherit;
  font-size: inherit;
  color: inherit;
  font-size: 30px;
  display: flex;
  align-items: center; ボタン内テキストを縦方向中央揃え 
  justify-content: center;  ボタン内テキストを横方向中央揃え 
} */

/* .share-icon {
  position: relative; 
  aspect-ratio: 1;
  object-fit: contain;
  object-position: center;
  width: 70px;
  height: auto;
  left: -40px;  
  top: -5px;  
} */




.return-button {
  display: flex;
  flex-direction: column;
  position: relative;
  border-radius: 30px;
  box-shadow: 4px 20px 4px rgba(0, 0, 0, 0.5);
  align-self: center;
  aspect-ratio: 1.777;
  margin-top: 20px;
  width: 100%;
  max-width: 295px;
  font-size: 48px;
  padding: 61px 33px;
  border: 1px solid rgba(0, 0, 0, 1); /* ボーダーを有効にする */
  background: none;
  cursor: pointer;
  font-family: inherit;
  color: inherit;
  overflow: hidden; /* アイコンがボタン外に出ないように調整 */
}

.return-icon {
  width: 100%;
  height: 100%;
  object-fit: cover; /* アイコンがボタン内で均等に表示されるように調整 */
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
}


.return-text {
  position: relative;
  z-index: 2;
  font-size: inherit;
  color: inherit;
  font-size: 45px;
  text-align: center;
}

.container {
  display: flex;
  flex-direction: column;
  gap: 15px;
  max-width: 300px;
  margin-top: 20px;
  width: 90%;
  margin-left: auto;
  margin-right: auto;
  font-size: 18px;
  font-family: 'Helvetica Neue', Arial, sans-serif;
}

.var-box {
  background: #fff; 
  border: 2px solid #333; 
  border-radius: 10px; 
  padding: 15px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
  line-height: 1.4;
  overflow-wrap: break-word;
  word-break: break-all;
  text-align: center; /* 全て中央揃えで統一 */
}

.var-box span {
  font-weight: bold;
  color: #000;
  display: block;
  margin-top: 5px;
}

.unified-box {
  background: rgba(255, 255, 255, 0.5); /* 白に近いグレーで透明度80% */  border: 1px solid #333; 
  border-radius: 10px; 
  padding: 10px 15px; /* 上下: 10px, 左右: 15px */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  line-height: 1.6;
  overflow-wrap: break-word;
  word-break: break-all;
  text-align: left; /* 左揃え */
  font-size: 18px;
  font-family: 'Helvetica Neue', Arial, sans-serif;

  width: 95%; /* 幅を100%に設定 */
  max-width: 450px; /* ここで親要素に依存せず最大幅を設定 */
  margin: 0 auto; /* 中央寄せ */
}



/* Token ID・他のボックスとの統一感を確保するため特別なスタイルは控える */
/* もし全て同じならこのセレクタは不要 */

/* Transaction Hash を少し読みやすくするための微調整のみ */





</style>