local composerReader = {}
local composerReader_mt = { __index = composerReader}
local json = require("json")
local jsonContents
function composerReader:loadGameScene(path)
	path = system.pathForFile(path,system.ResourceDirectory)
    local file = io.open(path,"r")
    local contents = nil
    if(file) then
        contents = file:read("*a")
     
    io.close(file)
    end
    if(contents~=nil)then
    	jsonContents = json.decode(contents)
    	
    end
   
end

function composerReader.createItemById(id)
	local jsonItem = getJsonById(id)
	
	if(jsonItem~=nil) then
		local object1 = display.newImage(jsonItem.imageFile)
		
		local object = display.newImageRect(jsonItem.imageFile,object1.contentWidth*jsonItem.xScale,object1.contentHeight*jsonItem.yScale)
		object1:removeSelf()
		object.contentScaleX = jsonItem.xScale
		object.contentScaleY = jsonItem.yScale
		
		object.linearDamping = jsonItem.linearDamping
		object.angularDamping  = jsonItem.angularDamping
		object.x = jsonItem.x
		object.y = jsonItem.y
		object.alpha = jsonItem.alpha
		object.rotation = jsonItem.rotation
		object.isVisible = jsonItem.isVisible
		if(jsonItem.physicsEnabled == true) then
			local objectShape = {}
			for i = 1,#jsonItem.bodyShape do
				objectShape[i*2-1] = jsonItem.bodyShape[i].x*jsonItem.xScale
				objectShape[i*2] = jsonItem.bodyShape[i].y*jsonItem.yScale
			
			end
			physics.addBody(object,jsonItem.bodyType,{density=jsonItem.density,friction=jsonItem.friction,bounce = jsonItem.bounce,radius = jsonItem.radius, shape=objectShape})
			object.isFixedRotation = jsonItem.isFixedRotation
			object.isSleepingAllowed = jsonItem.isSleepingAllowed
			object.isBodyActive = jsonItem.isBodyActive
			object.isBullet = jsonItem.isBullet
		end
		
		return object
	end
	
	return nil
end

function getJsonById(id)
		for index,value in pairs(jsonContents["objects"]) do
    		if(type(value) == "table") then
    			
    			if(jsonContents["objects"][index].id == id) then
    				return jsonContents["objects"][index]
    			end
    		end
    	end

    	return nil
end





return composerReader
