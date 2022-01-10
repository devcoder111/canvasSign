<template>
  <div>
    <div class="flex h-screen overflow-hidden bg-gray-100">
      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div class="flex items-center justify-center text-center h-full p-0">
          <div
            class="fixed inset-0 transition-opacity bg-gray-500 bg-opacity-75"
            aria-hidden="true"
          ></div>

          <!-- This element is to trick the browser into centering the modal contents. -->
          <!-- <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">​</span> -->

          <div
            class="inline-block rounded-sm h-screen shadow-xl transform transition-all sm:my-8 sm:align-middle w-screen overflow-y-auto"
          >
            <div class="w-full h-full">
              <div class="flex flex-col w-full xl:flex-row overflow-y-auto">
                <div class="flex items-center py-16 justify-center w-full">
                  <div class="relative">
                    <img
                      id="background"
                      class="object-contain"
                      src="~/assets/bg2.jpg"
                    />
                    <canvas
                      id="canvas"
                      class="w-full h-full absolute top-0 left-0"
                      v-on:mousedown="onCanvasMouseDown"
                      v-on:mousemove="onCanvasMouseMove"
                      v-on:mouseup="onCanvasMouseUp"
                      v-on:mouseleave="onCanvasMouseLeave"
                    ></canvas>
                  </div>
                </div>

                <div
                  class="relative flex items-start pt-10 justify-center h-screen xl:w-[600px] bg-white overflow-y-auto"
                >
                  <div>
                    <div class="flex items-center justify-around px-10 pb-10">
                      <button
                        v-on:click="clearEverything()"
                        class="inline-flex items-center self-end px-4 py-2 text-sm font-medium text-white border-transparent rounded-md shadow-sm bg-brand-blue border hover:bg-brand-blue-dark focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-brand-blue"
                      >
                        Clear everything
                      </button>
                      <button
                        v-on:click="removeLastStroke()"
                        class="inline-flex items-center self-end px-4 py-2 text-sm font-medium text-white border-transparent rounded-md shadow-sm bg-brand-blue border hover:bg-brand-blue-dark focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-brand-blue"
                      >
                        Remove last stroke
                      </button>
                    </div>
                    <div class="flex items-center justify-between px-10">
                      <div class="flex items-center space-x-2">
                        <svg
                          xmlns="http://www.w3.org/2000/svg"
                          class="h-6 w-6 text-gray-800"
                          fill="none"
                          viewBox="0 0 24 24"
                          stroke="currentColor"
                        >
                          <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z"
                          />
                        </svg>
                        <h4 class="text-xl font-bold text-gray-800">Comment</h4>
                      </div>
                    </div>

                    <div class="px-10 py-5">
                      <div>
                        <div class="flow-root">
                          <div
                            class="flex flex-col items-start space-y-4 border border-gray-800 rounded-md p-5 w-[400px]"
                          >
                            <div
                              class="flex items-start justify-between flex-shrink-0 w-full"
                            >
                              <div class="flex items-start">
                                <img
                                  class="inline-block w-10 h-10 rounded-full"
                                  src="https://images.unsplash.com/photo-1550525811-e5869dd03032?ixlib=rb-1.2.1&amp;ixid=eyJhcHBfaWQiOjEyMDd9&amp;auto=format&amp;fit=facearea&amp;facepad=2&amp;w=256&amp;h=256&amp;q=80"
                                  alt=""
                                />
                                <textarea
                                  rows="3"
                                  name="comment"
                                  id="comment"
                                  class="w-full resize-none focus:ring-0 sm:text-sm appearance-none w-[220px] h-[90px]"
                                  placeholder="Add your comment..."
                                  v-model="comment"
                                ></textarea>
                              </div>

                              <div class="flex items-center ml-auto space-x-5">
                                <div class="flex items-center">
                                  <div class="relative inline-block text-left">
                                    <div>
                                      <button
                                        type="button"
                                        class="inline-flex justify-center text-gray-500"
                                        id="menu-button"
                                        v-on:click="toggleColorPane()"
                                      >
                                        <svg
                                          xmlns="http://www.w3.org/2000/svg"
                                          class="w-5"
                                          fill="none"
                                          viewBox="0 0 24 24"
                                          stroke="currentColor"
                                        >
                                          <path
                                            stroke-linecap="round"
                                            stroke-linejoin="round"
                                            stroke-width="2"
                                            d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z"
                                          />
                                        </svg>
                                        <svg
                                          class="w-5 h-5 ml-2 -mr-1"
                                          xmlns="http://www.w3.org/2000/svg"
                                          viewBox="0 0 20 20"
                                          fill="currentColor"
                                          aria-hidden="true"
                                        >
                                          <path
                                            fill-rule="evenodd"
                                            d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                                            clip-rule="evenodd"
                                          ></path>
                                        </svg>
                                      </button>
                                    </div>

                                    <div
                                      class="absolute right-0 z-40 w-16 py-4 mt-2 bg-white origin-top-right text-gray-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
                                      role="menu"
                                      aria-orientation="vertical"
                                      aria-labelledby="menu-button"
                                      tabindex="-1"
                                      v-show="isColorPaneVisible"
                                    >
                                      <div
                                        class="flex flex-col items-center space-y-3 bg-white z-30"
                                        role="none"
                                      >
                                        <button
                                          v-for="(color, index) in colors"
                                          v-bind:key="index"
                                          v-on:click="selectColor(index)"
                                          v-bind:style="{
                                            backgroundColor: color,
                                          }"
                                          class="block w-5 h-5 rounded-full"
                                        ></button>
                                      </div>
                                    </div>
                                  </div>
                                </div>

                                <div class="flex items-center">
                                  <button
                                    type="button"
                                    class="-m-2.5 w-10 h-10 rounded-full inline-flex items-center justify-center text-gray-400 hover:text-gray-500"
                                  >
                                    <span class="sr-only">Mention someone</span>
                                    <svg
                                      xmlns="http://www.w3.org/2000/svg"
                                      class="w-6 h-6"
                                      fill="none"
                                      viewBox="0 0 24 24"
                                      stroke="currentColor"
                                    >
                                      <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12"
                                      />
                                    </svg>
                                  </button>
                                </div>
                              </div>
                            </div>
                            <div class="flex-1 w-full p-0">
                              <form action="#" class="relative p-0">
                                <div class="flex justify-end">
                                  <div
                                    class="flex items-end justify-end flex-shrink-0 space-x-2"
                                  >
                                    <button
                                      type="button"
                                      class="text-black py-2 hover:underline"
                                    >
                                      Cancel
                                    </button>

                                    <button
                                      class="inline-flex items-center self-end px-4 py-2 text-sm font-medium text-white border-transparent rounded-md shadow-sm bg-brand-blue border hover:bg-brand-blue-dark focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-brand-blue"
                                      v-on:click.prevent="postComment()"
                                    >
                                      Post
                                    </button>
                                  </div>
                                </div>
                              </form>
                            </div>
                          </div>

                          <div class="flex flex-col">
                            <div
                              class="overflow-y-auto divide-y divide-gray-700"
                              v-for="(item, index) in comments"
                              v-bind:key="index"
                            >
                              <div class="py-5 flex">
                                <img
                                  src="https://images.unsplash.com/photo-1550525811-e5869dd03032?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
                                  alt="Emily Selman."
                                  class="w-12 h-12 rounded-full flex-shrink-0"
                                />
                                <div class="flex flex-col ml-3 w-full">
                                  <h4
                                    class="text-sm font-bold text-gray-700 text-left"
                                  >
                                    Emily Selman
                                  </h4>

                                  <div
                                    class="flex items-center space-x-2 text-base text-gray-500 text-left"
                                  >
                                    <p class="w-full break-all">
                                      {{ item }}
                                    </p>
                                    <button class="px-5 text-gray-400 hidden">
                                      <svg
                                        xmlns="http://www.w3.org/2000/svg"
                                        class="w-6 h-6"
                                        fill="none"
                                        viewBox="0 0 24 24"
                                        stroke="currentColor"
                                      >
                                        <path
                                          stroke-linecap="round"
                                          stroke-linejoin="round"
                                          stroke-width="2"
                                          d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
                                        />
                                      </svg>
                                    </button>
                                  </div>
                                </div>
                              </div>
                            </div>
                            <div class="hidden">
                              <button
                                class="flex items-center mt-2 space-x-1 text-sm text-gray-400"
                              >
                                <svg
                                  xmlns="http://www.w3.org/2000/svg"
                                  class="w-5 h-5"
                                  viewBox="0 0 20 20"
                                  fill="currentColor"
                                >
                                  <path
                                    fill-rule="evenodd"
                                    d="M7.707 3.293a1 1 0 010 1.414L5.414 7H11a7 7 0 017 7v2a1 1 0 11-2 0v-2a5 5 0 00-5-5H5.414l2.293 2.293a1 1 0 11-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
                                    clip-rule="evenodd"
                                  />
                                </svg>
                                <span>Reply</span>
                              </button>
                              <div class="w-full mt-4">
                                <div
                                  class="flex items-center px-5 border border-gray-800 rounded relative"
                                >
                                  <img
                                    class="inline-block w-10 h-10 rounded-full"
                                    src="https://images.unsplash.com/photo-1550525811-e5869dd03032?ixlib=rb-1.2.1&amp;ixid=eyJhcHBfaWQiOjEyMDd9&amp;auto=format&amp;fit=facearea&amp;facepad=2&amp;w=256&amp;h=256&amp;q=80"
                                    alt=""
                                  />

                                  <form
                                    action="#"
                                    class="inline flex space-x-2 justify-between items-center w-full"
                                  >
                                    <textarea
                                      name="comment"
                                      id="comment"
                                      rows="1"
                                      class="block w-full resize-none border-0 focus:ring-0 sm:text-sm py-4"
                                      placeholder="Add your comment..."
                                    ></textarea>

                                    <div
                                      class="bg-gray-800 text-white rounded w-16 px-1 inline -mt-16 right-0 absolute"
                                    >
                                      Upload
                                    </div>
                                    <button>
                                      <svg
                                        xmlns="http://www.w3.org/2000/svg"
                                        class="h-6 w-6"
                                        fill="none"
                                        viewBox="0 0 24 24"
                                        stroke="currentColor"
                                      >
                                        <path
                                          stroke-linecap="round"
                                          stroke-linejoin="round"
                                          stroke-width="2"
                                          d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"
                                        />
                                      </svg>
                                    </button>
                                  </form>
                                </div>
                              </div>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      canvas: null,
      ctx: null,
      isMouseDown: false,
      isColorPaneVisible: false,
      color: "#DC2626",
      colors: ["#DC2626", "#16A34A", "#CA8A04", "#2563EB", "#4F46E5"],
      segments: [],
      comments: [],
      comment: "",
    };
  },
  methods: {
    clearEverything: function () {
      this.segments = [];
      this.redraw();
    },
    removeLastStroke: function () {
      this.segments.pop();
      this.redraw();
    },
    redraw: function () {
      let i, segment, points, j, pl;
      const l = this.segments.length;
      this.ctx.lineCap = "round";
      this.ctx.lineJoin = "round";
      this.ctx.lineWidth = 10;
      this.ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (i = 0; i < l; i++) {
        segment = this.segments[i];
        points = segment.points;
        this.ctx.strokeStyle = segment.color;
        this.ctx.beginPath();
        this.ctx.moveTo(points[0].x, points[0].y);
        pl = points.length;
        for (j = 0; j < pl; j++) {
          this.ctx.lineTo(points[j].x, points[j].y);
        }
        this.ctx.stroke();
        this.ctx.closePath();
      }
    },
    postComment: function () {
      this.comments.push(this.comment);
      this.comment = "";
    },
    toggleColorPane: function () {
      this.isColorPaneVisible = !this.isColorPaneVisible;
    },
    selectColor: function (index) {
      this.color = this.colors[index];
      this.isColorPaneVisible = false;
    },
    onCanvasMouseDown: function (event) {
      this.segments.push({
        color: this.color,
        points: [
          {
            x:
              (event.offsetX * this.canvas.width) /
              document.getElementById("background").offsetWidth,
            y:
              (event.offsetY * this.canvas.height) /
              document.getElementById("background").offsetHeight,
          },
        ],
      });
      this.isMouseDown = true;
    },
    onCanvasMouseMove: function (event) {
      if (this.isMouseDown) {
        this.segments[this.segments.length - 1].points.push({
          x:
            (event.offsetX * this.canvas.width) /
            document.getElementById("background").offsetWidth,
          y:
            (event.offsetY * this.canvas.height) /
            document.getElementById("background").offsetHeight,
        });
        this.draw();
      }
    },
    onCanvasMouseUp: function (event) {
      this.isMouseDown = false;
    },
    onCanvasMouseLeave: function (event) {
      this.isMouseDown = false;
    },
    draw: function () {
      var points = this.segments[this.segments.length - 1].points;
      this.ctx.lineCap = "round";
      this.ctx.lineJoin = "round";
      this.ctx.lineWidth = 10;
      this.ctx.strokeStyle = this.color;
      this.ctx.beginPath();
      this.ctx.moveTo(points[points.length - 2].x, points[points.length - 2].y);
      this.ctx.lineTo(points[points.length - 1].x, points[points.length - 1].y);
      this.ctx.stroke();
      this.ctx.closePath();
    },
  },
  mounted() {
    this.canvas = document.getElementById("canvas");
    this.ctx = this.canvas.getContext("2d");
    var background = document.getElementById("background");
    background.onload = () => {
      this.canvas.setAttribute("width", background.offsetWidth);
      this.canvas.setAttribute("height", background.offsetHeight);
    };
  },
};
</script>
