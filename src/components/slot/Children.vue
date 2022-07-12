<template>
    <div> 
        这是每个复用该组件都显示的
        <slot></slot>
        <slot name="slot1"></slot>
        <slot name="slot2"></slot>
        <slot name="slot3"></slot>
        <slot name="slot4">这是一个备用插槽内容</slot>
    </div>
</template>