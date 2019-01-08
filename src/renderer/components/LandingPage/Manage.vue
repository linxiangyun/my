<template>
        <div>
        <Steps current="0">
        <Step title="需求背景"></Step>
            <Step title="功能测试分析"></Step>
            <Step title="专项测试分析"></Step>
            <Step title="用户场景分析"></Step>
            <Step title="完成"></Step>
        </Steps>
        <Input v-model="TextValue" type="textarea" placeholder="需求背景描述" />
        <!-- <Button type="primary" @click="next">{{ButtonName}}</Button> -->
        </div>
</template>