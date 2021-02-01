<template>
  <div class="carousel">
    <transition-group :name="direction">
    <slide
      v-for="(data, index) in carouselData"
      :key="index"
      :image="data.image"
      :text="data.text"
      v-show="index === currentIndex"
    />
    </transition-group>
    <div class="carousel__buttons">
      <button @click="goLeft" v-if="currentIndex !== 0" class="left-btn">
        <i class="fas fa-angle-left"></i>
      </button>
      <button
        @click="goRight"
        v-if="currentIndex < carouselData.length - 1"
        class="right-btn"
      >
        <i class="fas fa-angle-right"></i>
      </button>
    </div>
    <div class="carousel__indicators">
      <button
        v-for="(item, index) in carouselData.length"
        :key="index"
        :class="currentIndex == index ? 'active' : ''"
        @click="goToIndex(index)"
      ></button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import Slide from "./Slide.vue";
export default {
  components: { Slide },
  setup() {
    const carouselData = [
      {
        image:
          "https://images.pexels.com/photos/1447092/pexels-photo-1447092.png?crop=entropy&cs=srgb&dl=pexels-thanhhoa-tran-1447092.jpg&fit=crop&fm=jpg&h=720&w=1280",
        text: "First",
      },
      {
        image:
          "https://images.pexels.com/photos/3408744/pexels-photo-3408744.jpeg?crop=entropy&cs=srgb&dl=pexels-stein-egil-liland-3408744.jpg&fit=crop&fm=jpg&h=813&w=1280",
        text: "Second",
      },
      {
        image:
          "https://images.pexels.com/photos/1004665/pexels-photo-1004665.jpeg?crop=entropy&cs=srgb&dl=pexels-eberhard-grossgasteiger-1004665.jpg&fit=crop&fm=jpg&h=853&w=1280",
        text: "Third",
      },
      {
        image:
          "https://images.pexels.com/photos/2166711/pexels-photo-2166711.jpeg?crop=entropy&cs=srgb&dl=pexels-quang-nguyen-vinh-2166711.jpg&fit=crop&fm=jpg&h=853&w=1280",
        text: "Fourth",
      },
      {
        image:
          "https://images.pexels.com/photos/858115/pexels-photo-858115.jpeg?crop=entropy&cs=srgb&dl=pexels-eberhard-grossgasteiger-858115.jpg&fit=crop&fm=jpg&h=853&w=1280",
        text: "Fifth",
      },
    ];

    let currentIndex = ref(0);
    let direction = ref('left')

    const goLeft = () => {
      direction.value = 'left'
      currentIndex.value -= 1;
    };

    const goRight = () => {
      direction.value = 'right'
      currentIndex.value += 1;
    };

    const goToIndex = (index) => {
      if(index < currentIndex.value) {
        direction.value = 'left'
      }
      else if (index > currentIndex.value) {
        direction.value = 'right'
      }
      currentIndex.value = index;
    };
    return {
      carouselData,
      currentIndex,
      goLeft,
      goRight,
      goToIndex,
      direction
    };
  },
};
</script>

<style>
.carousel {
  height: 100vh;
  position: relative;
}

.carousel__buttons .left-btn,
.carousel__buttons .right-btn {
  background: rgba(0, 0, 0, 0.5);
  color: #fff;
  border: 0;
  outline: 0;
  padding: 10px;
  cursor: pointer;

  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}

.carousel__buttons i {
  font-size: 24px;
}

.left-btn {
  left: 0;
}

.right-btn {
  right: 0;
}

.carousel__indicators {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0, 0, 0, 0.8);
  padding: 10px 15px;

  display: flex;
  justify-content: space-between;
  align-items: center;
}

.carousel__indicators button {
  background: rgba(255, 255, 255, 0.5);
  outline: none;
  border: 0;
  cursor: pointer;
  height: 12px;
  width: 12px;
  border-radius: 4px;
  margin: 0 8px;
}

.carousel__indicators button:hover {
  background: rgba(255, 255, 255, 0.8);
}
.carousel__indicators button.active {
  background: #fff;
}
.left-enter-active {
  animation: leftInAnim 0.4s ease-in-out;
}

.left-leave-active {
  animation: leftOutAnim 0.4s ease-in-out;
}

.left-enter-active,.left-leave-active {
  position: absolute;
}

@keyframes leftInAnim {
  from {
    transform: translateX(-100%);
  }

  to {
    transform: translateX(0%);
  }
}

@keyframes leftOutAnim {
  from {
    transform: translateX(0%);
  }

  to {
    transform: translateX(100%);
  }
}

.right-enter-active {
  animation: rightInAnim 0.4s ease-in-out;
}

.right-leave-active {
  animation: rightOutAnim 0.4s ease-in-out;
}

.right-leave-active,
.right-enter-active {
  position: absolute;
}

@keyframes rightInAnim {
  from {
    transform: translateX(100%);
  }

  to {
    transform: translateX(0%);
  }
}

@keyframes rightOutAnim {
  from {
    transform: translateX(0%);
  }

  to {
    transform: translateX(-100%);
  }
}

</style>
