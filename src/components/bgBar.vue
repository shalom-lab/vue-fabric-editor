<template>
  <div v-if="!mixinState.mSelectMode">
    <Divider orientation="left" plain>{{ $t('color') }}</Divider>
    <Form :label-width="40">
      <FormItem :label="$t('color')" prop="name">
        <ColorPicker v-model="color" @on-change="setThisColor" alpha size="small" transfer />
      </FormItem>
    </Form>
    <Divider orientation="left" plain>{{ $t('color_macthing') }}</Divider>
    <div class="color-list">
      <template v-for="(item, i) in colorList" :key="item.label + i">
        <div class="item">
          {{ item.label }}:
          <span
            v-for="color in item.color"
            :key="color"
            :style="`background:${color}`"
            @click="setColor(color)"
          ></span>
        </div>
      </template>
    </div>
  </div>
</template>

<script setup name="BgBar">
import { ref } from 'vue';
import useSelect from '@/hooks/select';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const { mixinState, canvasEditor } = useSelect();

const colorList = [
  {
    label: t('scenary_x', { number: 1 }),
    color: ['#86DCCD', '#E7FDCB', '#FFDC84', '#F57677', '#5FC2C7', '#98DFE5', '#C2EFF3', '#DDFDFD'],
  },
  {
    label: t('scenary_x', { number: 2 }),
    color: ['#9EE9D3', '#2FC6C8', '#2D7A9D', '#48466d', '#61c0bf', '#bbded6', '#fae3d9', '#ffb6b9'],
  },
  {
    label: t('scenary_x', { number: 3 }),
    color: ['#f8fafc', '#f1f5f9', '#e2e8f0', '#cbd5e1', '#94a3b8', '#64748b', '#475569', '#334155'],
  },
  {
    label: t('scenary_x', { number: 4 }),
    color: ['#f9fafb', '#f3f4f6', '#e5e7eb', '#d1d5db', '#9ca3af', '#6b7280', '#4b5563', '#374151'],
  },
  {
    label: t('scenary_x', { number: 5 }),
    color: ['#fafafa', '#f4f4f5', '#e4e4e7', '#d4d4d8', '#a1a1aa', '#71717a', '#52525b', '#3f3f46'],
  },
  {
    label: t('scenary_x', { number: 6 }),
    color: ['#fafafa', '#f5f5f5', '#e5e5e5', '#d4d4d4', '#a3a3a3', '#737373', '#525252', '#404040'],
  },
  {
    label: t('scenary_x', { number: 7 }),
    color: ['#fafaf9', '#f5f5f4', '#e7e5e4', '#d6d3d1', '#a8a29e', '#78716c', '#57534e', '#44403c'],
  },
  {
    label: t('scenary_x', { number: 8 }),
    color: ['#fef2f2', '#fee2e2', '#fecaca', '#fca5a5', '#f87171', '#ef4444', '#dc2626', '#b91c1c'],
  },
  {
    label: t('scenary_x', { number: 9 }),
    color: ['#fff7ed', '#ffedd5', '#fed7aa', '#fdba74', '#fb923c', '#f97316', '#ea580c', '#c2410c'],
  },
  {
    label: t('scenary_x', { number: 10 }),
    color: ['#fffbeb', '#fef3c7', '#fde68a', '#fcd34d', '#fbbf24', '#f59e0b', '#d97706', '#b45309'],
  },
  {
    label: t('scenary_x', { number: 11 }),
    color: ['#fefce8', '#fef9c3', '#fef08a', '#fde047', '#facc15', '#eab308', '#ca8a04', '#a16207'],
  },
  {
    label: t('scenary_x', { number: 12 }),
    color: ['#f7fee7', '#ecfccb', '#d9f99d', '#bef264', '#a3e635', '#84cc16', '#65a30d', '#4d7c0f'],
  },
  {
    label: t('scenary_x', { number: 13 }),
    color: ['#f0fdf4', '#dcfce7', '#bbf7d0', '#86efac', '#4ade80', '#22c55e', '#16a34a', '#15803d'],
  },
  {
    label: t('scenary_x', { number: 14 }),
    color: ['#ecfdf5', '#d1fae5', '#a7f3d0', '#6ee7b7', '#34d399', '#10b981', '#059669', '#047857'],
  },
  {
    label: t('scenary_x', { number: 15 }),
    color: ['#f0fdfa', '#ccfbf1', '#99f6e4', '#5eead4', '#2dd4bf', '#14b8a6', '#0d9488', '#0f766e'],
  },
  {
    label: t('scenary_x', { number: 16 }),
    color: ['#ecfeff', '#cffafe', '#a5f3fc', '#67e8f9', '#22d3ee', '#06b6d4', '#0891b2', '#0e7490'],
  },
  {
    label: t('scenary_x', { number: 17 }),
    color: ['#f0f9ff', '#e0f2fe', '#bae6fd', '#7dd3fc', '#38bdf8', '#0ea5e9', '#0284c7', '#0369a1'],
  },
  {
    label: t('scenary_x', { number: 18 }),
    color: ['#eff6ff', '#dbeafe', '#bfdbfe', '#93c5fd', '#60a5fa', '#3b82f6', '#2563eb', '#1d4ed8'],
  },
  {
    label: t('scenary_x', { number: 19 }),
    color: ['#eef2ff', '#e0e7ff', '#c7d2fe', '#a5b4fc', '#818cf8', '#6366f1', '#4f46e5', '#4338ca'],
  },
  {
    label: t('scenary_x', { number: 20 }),
    color: ['#f5f3ff', '#ede9fe', '#ddd6fe', '#c4b5fd', '#a78bfa', '#8b5cf6', '#7c3aed', '#6d28d9'],
  },
  {
    label: t('scenary_x', { number: 21 }),
    color: ['#faf5ff', '#f3e8ff', '#e9d5ff', '#d8b4fe', '#c084fc', '#a855f7', '#9333ea', '#7e22ce'],
  },
  {
    label: t('scenary_x', { number: 22 }),
    color: ['#fdf4ff', '#fae8ff', '#f5d0fe', '#f0abfc', '#e879f9', '#d946ef', '#c026d3', '#a21caf'],
  },
  {
    label: t('scenary_x', { number: 23 }),
    color: ['#fdf2f8', '#fce7f3', '#fbcfe8', '#f9a8d4', '#f472b6', '#ec4899', '#db2777', '#be185d'],
  },
  {
    label: t('scenary_x', { number: 24 }),
    color: ['#fff1f2', '#ffe4e6', '#fecdd3', '#fda4af', '#fb7185', '#f43f5e', '#e11d48', '#be123c'],
  },
];

const color = ref('');
// 背景颜色设置
const setThisColor = () => {
  setColor(color.value);
};
// 背景颜色设置
function setColor(color) {
  const workspace = canvasEditor.canvas.getObjects().find((item) => item.id === 'workspace');
  workspace.set('fill', color);
  canvasEditor.canvas.renderAll();
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
:deep(.ivu-form-item) {
  margin-bottom: 0;
}
.img {
  width: 50px;
  padding: 5px;
  background: #f5f5f5;
  margin-left: 2px;
  height: 70px;
  cursor: pointer;
}

.color-list {
  padding: 10px 0;
  .item {
    padding-bottom: 5px;
  }
  span {
    display: inline-block;
    margin-left: 6px;
    background: #f5f5f5;
    height: 20px;
    width: 20px;
    font-size: 12px;
    line-height: 20px;
    vertical-align: middle;
    cursor: pointer;
  }
}

:deep(.ivu-divider-plain) {
  &.ivu-divider-with-text-left {
    margin: 10px 0;
    font-weight: bold;
  }
}
</style>
