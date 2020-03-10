<template>
  <div>
    <div class="d-flex">
      <div class="text--secondary">
        {{ label }}
      </div>
      <div class="ml-auto">
        <slot name="append-outer" />
      </div>
    </div>
    <div>
      <no-ssr>
        <codemirror
          :value="value"
          :readonly="readonly"
          :options="options"
          @input="$emit('input', $event)"
        />
      </no-ssr>
    </div>
  </div>
</template>

<script>
import { codemirror } from "vue-codemirror";
import NoSSR from "vue-no-ssr";
import "codemirror/lib/codemirror.css";
// language
import "codemirror/mode/jinja2/jinja2.js";
import "codemirror/mode/javascript/javascript.js";

// active-line.js
import "codemirror/addon/selection/active-line.js";

// styleSelectedText
import "codemirror/addon/selection/mark-selection.js";
import "codemirror/addon/search/searchcursor.js";

// highlightSelectionMatches
import "codemirror/addon/scroll/annotatescrollbar.js";
import "codemirror/addon/search/matchesonscrollbar.js";

import "codemirror/addon/search/match-highlighter.js";

// keyMap
import "codemirror/mode/clike/clike.js";
import "codemirror/addon/edit/matchbrackets.js";
import "codemirror/addon/comment/comment.js";
import "codemirror/addon/dialog/dialog.js";
import "codemirror/addon/dialog/dialog.css";

import "codemirror/addon/search/search.js";
import "codemirror/keymap/sublime.js";

// foldGutter
import "codemirror/addon/fold/foldgutter.css";
import "codemirror/addon/fold/brace-fold.js";
import "codemirror/addon/fold/comment-fold.js";
import "codemirror/addon/fold/foldcode.js";
import "codemirror/addon/fold/foldgutter.js";
import "codemirror/addon/fold/indent-fold.js";
import "codemirror/addon/fold/markdown-fold.js";
import "codemirror/addon/fold/xml-fold.js";

export default {
  components: {
    codemirror,
    "no-ssr": NoSSR
  },
  props: {
    value: {
      type: String,
      default: ""
    },
    language: {
      type: String,
      default: "none"
    },
    label: {
      type: String,
      default: "none"
    },
    readonly: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      options: {
        tabSize: 4,
        foldGutter: true,
        styleActiveLine: true,
        lineNumbers: true,
        line: true,
        keyMap: "sublime",
        mode: this.language,
        readOnly: this.readonly,
        theme: "neo",
        extraKeys: {
          F11(cm) {
            cm.setOption("fullScreen", !cm.getOption("fullScreen"));
          },
          Esc(cm) {
            if (cm.getOption("fullScreen")) {
              cm.setOption("fullScreen", false);
            }
          }
        }
      }
    };
  }
};
</script>

<style type="scss">
.CodeMirror {
  height: auto;
}
</style>
