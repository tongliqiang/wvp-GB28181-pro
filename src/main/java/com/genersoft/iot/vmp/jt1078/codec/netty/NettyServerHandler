package com.genersoft.iot.vmp.jt1078.codec.netty;

import io.netty.channel.Channel;
import io.netty.channel.ChannelHandlerContext;
import io.netty.channel.SimpleChannelInboundHandler;
import io.netty.channel.group.ChannelGroup;
import io.netty.channel.group.DefaultChannelGroup;
import io.netty.util.concurrent.GlobalEventExecutor;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class NettyServerHandler extends SimpleChannelInboundHandler<String> {

    private final Logger logger = LoggerFactory.getLogger(NettyServerHandler.class);
    //定义一个channle 组，管理所有的channel
    //GlobalEventExecutor.INSTANCE) 是全局的事件执行器，是一个单例
    public static ChannelGroup channelGroup = new DefaultChannelGroup(GlobalEventExecutor.INSTANCE);
 
    /**
     * 有客户端与服务器发生连接时执行此方法
     * 1.打印提示信息
     * 2.将客户端保存到 channelGroup 中
     */
    @Override
    public void handlerAdded(ChannelHandlerContext ctx) throws Exception {
        Channel channel = ctx.channel();
        logger.info("有新的客户端与服务器发生连接。客户端地址：" + channel.remoteAddress());
        channelGroup.add(channel);
    }
 
    /**
     * 当有客户端与服务器断开连接时执行此方法，此时会自动将此客户端从 channelGroup 中移除
     * 1.打印提示信息
     */
    @Override
    public void handlerRemoved(ChannelHandlerContext ctx) throws Exception {
        Channel channel = ctx.channel();
        logger.error("有客户端与服务器断开连接。客户端地址：" + channel.remoteAddress());
    }
 
    /**
     * 表示channel 处于活动状态
     */
    @Override
    public void channelActive(ChannelHandlerContext ctx) throws Exception {
        logger.info(ctx.channel().remoteAddress() + " 处于活动状态");
    }
 
    /**
     * 表示channel 处于不活动状态
     */
    @Override
    public void channelInactive(ChannelHandlerContext ctx) throws Exception {
        logger.info(ctx.channel().remoteAddress() + " 处于不活动状态");
    }
 
    /**
     * 读取到客户端发来的数据数据
     */
    @Override
    protected void channelRead0(ChannelHandlerContext ctx, String msg) {
        //获取到当前channel
        Channel channel = ctx.channel();
        logger.info("有客户端发来的数据。地址：" + channel.remoteAddress() + " 内容：" + msg);
    }
 
    /**
     * 处理异常
     */
    @Override
    public void exceptionCaught(ChannelHandlerContext ctx, Throwable cause) throws Exception {
        logger.error("发生异常。异常信息：{}", cause.getMessage());
        //关闭通道
        ctx.close();
    }
}
